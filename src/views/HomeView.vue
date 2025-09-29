<template>
  <main class="home">
    <h1 class="home__title">Lista de Personajes</h1>

    <input
      type="text"
      v-model="busqueda"
      placeholder="Buscar personaje..."
      class="home__search"
      aria-label="Buscar personaje por nombre"
    />

    <section class="home__list">
      <PersonajeCard
        v-for="personaje in personajesFiltrados"
        :key="personaje.id"
        :nombre="personaje.nombre"
        :descripcion="personaje.descripcion"
        :imagen="personaje.imagen"
      />
    </section>
  </main>
</template>

<script>
import PersonajeCard from '../components/PersonajeCard.vue'
import personajesData from '../data/personajes.js'

export default {
  components: { PersonajeCard },
  data() {
    return {
      personajes: personajesData.personajes,
      busqueda: ''
    }
  },
  computed: {
    personajesFiltrados() {
      return this.personajes.filter(p =>
        p.nombre.toLowerCase().includes(this.busqueda.toLowerCase())
      )
    }
  }
}
</script>

<style scoped>
.home {
  padding: 2rem;
  background-color: #f2f2f2;
  min-height: 100vh;
}
.home__title {
  font-size: 2rem;
  margin-bottom: 1rem;
  color: #ef5350;
  text-align: center;
}
.home__search {
  display: block;
  margin: 0 auto 2rem;
  padding: 0.5rem 1rem;
  font-size: 1rem;
  border: 2px solid #2a75bb;
  border-radius: 8px;
  width: 300px;
}
.home__list {
  display: flex;
  flex-wrap: wrap;
  gap: 1.5rem;
  justify-content: center;
}
</style>
