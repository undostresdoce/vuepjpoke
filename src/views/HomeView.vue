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

    <select v-model="tipoSeleccionado" class="home__filter" aria-label="Filtrar por tipo">
      <option value="">Todos los tipos</option>
      <option v-for="tipo in tiposDisponibles" :key="tipo" :value="tipo">
        {{ tipo }}
      </option>
    </select>

    <button @click="invertirOrden" class="home__ordenar">
      Ordenar: {{ ordenAscendente ? 'A-Z' : 'Z-A' }}
    </button>

    <p class="home__contador">
      {{ personajesFiltrados.length }} resultados encontrados
    </p>

    <transition-group name="fade" tag="section" class="home__list">
      <PersonajeCard
        v-for="personaje in personajesFiltrados"
        :key="personaje.id"
        :nombre="personaje.nombre"
        :descripcion="personaje.descripcion"
        :imagen="personaje.imagen"
      />
    </transition-group>

    <p v-if="personajesFiltrados.length === 0" class="home__no-result">
      El pokémon que desea buscar no existe.
    </p>
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
      busqueda: '',
      tipoSeleccionado: '',
      ordenAscendente: true
    }
  },
  computed: {
    tiposDisponibles() {
      return [...new Set(this.personajes.map(p => p.tipo))].sort()
    },
    personajesFiltrados() {
      let filtrados = this.personajes.filter(p =>
        p.nombre.toLowerCase().includes(this.busqueda.toLowerCase())
      )

      if (this.tipoSeleccionado) {
        filtrados = filtrados.filter(p => p.tipo === this.tipoSeleccionado)
      }

      filtrados.sort((a, b) => {
        const nombreA = a.nombre.toLowerCase()
        const nombreB = b.nombre.toLowerCase()
        return this.ordenAscendente
          ? nombreA.localeCompare(nombreB)
          : nombreB.localeCompare(nombreA)
      })

      return filtrados
    }
  },
  watch: {
    busqueda(nuevaBusqueda) {
      if (nuevaBusqueda.trim() === '') {
        console.warn('Campo de búsqueda vacío')
      }
    }
  },
  methods: {
    invertirOrden() {
      this.ordenAscendente = !this.ordenAscendente
    }
  }
}
</script>

<style scoped>
.home {
  padding: 2rem;
  background-color: #f2f2f2;
}
.home__title {
  font-size: 2rem;
  margin-bottom: 1rem;
  color: #ef5350;
  text-align: center;
}
.home__search,
.home__filter {
  display: block;
  margin: 0 auto 1rem;
  padding: 0.5rem 1rem;
  font-size: 1rem;
  border: 2px solid #2a75bb;
  border-radius: 8px;
  width: 300px;
}
.home__ordenar {
  display: block;
  margin: 0 auto 1rem;
  background-color: #2a75bb;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 8px;
  cursor: pointer;
}
.home__contador {
  text-align: center;
  font-weight: bold;
  margin-bottom: 1rem;
}
.home__list {
  display: flex;
  flex-wrap: wrap;
  gap: 1.5rem;
  justify-content: center;
}
.home__no-result {
  text-align: center;
  font-weight: bold;
  color: #ef5350;
  margin-top: 2rem;
}

/* Transición suave */
.fade-enter-active,
.fade-leave-active {
  transition: all 0.5s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(10px);
}
</style>
