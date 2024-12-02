
<script setup>
  defineProps({
    title: String,
    body: String,
    image: String // Prop para la imagen del póster
  });
</script>

<template>
  <div class="card" style="width: 18rem;">
    <img :src="image" class="card-img-top" alt="Movie Poster">
    <div class="card-body">
      <h5 class="card-title">{{ title }}</h5>
      <p class="card-text">{{ body }}</p>
    </div>
  </div>
</template>

