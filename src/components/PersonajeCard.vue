<template>
  <article class="card" :aria-label="`Personaje: ${nombre}`" role="region">
    <img :src="imagen" :alt="`Imagen de ${nombre}`" class="card__img" />
    <h2 class="card__name">{{ nombre }}</h2>
    <p class="card__desc">{{ descripcion }}</p>
  </article>
</template>

<script>
export default {
  props: {
    nombre: { type: String, required: true },
    descripcion: { type: String, required: true },
    imagen: { type: String, required: false }
  }
}
</script>

<style scoped>
.card {
  background-color: #fff;
  border: 2px solid #ffcb05;
  border-radius: 12px;
  padding: 1rem;
  width: 220px;
  text-align: center;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  transition: transform 0.3s ease;
}
.card:hover {
  transform: scale(1.05);
}
.card__img {
  width: 100px;
  height: auto;
  margin-bottom: 0.5rem;
}
.card__name {
  font-size: 1.2rem;
  font-weight: bold;
  color: #2a75bb;
}
.card__desc {
  font-size: 0.95rem;
  color: #555;
}
</style>
