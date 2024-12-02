<script setup>
import { ref } from 'vue';
import MovieCard from './Movies/Components/MovieCard.vue';

const movies = ref([]); // Lista de películas
const valor = 10; 
const inicio = ref(0); // Índice inicial de la paginación
const fin = ref(10); 
const getMovies = async () => {
  try {
    const resp = await fetch('https://api.themoviedb.org/3/movie/popular?api_key=1d0e6e1e3eaa2ea344d894e438f72919&language=es&page=1');
    const data = await resp.json();
    movies.value = data.results; 
  } catch (error) {
    console.error('Error movies:', error);
  }
};

const nextMovies = () => {
  if (fin.value < movies.value.length) {
    inicio.value += valor;
    fin.value += valor;
  }
};

const backMovies = () => {
  if (inicio.value > 0) {
    inicio.value -= valor;
    fin.value -= valor;
  }
};

getMovies();
</script>

<template>
  <div>
    <h3 class="text-center text-primary">Popular Movies</h3>
    
    <div class="d-flex justify-content-center mb-3">
      <button class="btn btn-primary me-3" @click="backMovies" :disabled="inicio <= 0"> Back</button>
      <button class="btn btn-primary" @click="nextMovies" :disabled="fin >= movies.length"> Next</button>
    </div>

    <div class="row">
      <MovieCard 
        v-for="movie in movies.slice(inicio, fin)" 
        :key="movie.id" 
        :title="movie.title" 
        :body="movie.overview" 
        :image="`https://image.tmdb.org/t/p/w500/${movie.poster_path} `" 
      />
    </div>
  </div>
</template>

