<script setup>
import { ref, computed } from 'vue'
import TaskForm from './components/TaskForm.vue'
import TaskList from './components/TaskList.vue'

// Estat global (component pare)
const tasques = ref([
  { id: 1, nom: 'Tasca 1', completada: true },
  { id: 2, nom: 'Tasca 2', completada: false },
  { id: 3, nom: 'Tasca 3', completada: false },
  { id: 4, nom: 'Tasca 4', completada: false }
])

const mostrarPendents = ref(false)

// Funcions de lògica principal
const afegirTasca = (nom) => {
  if (nom.trim() === '') return
  let nouId = tasques.value.length > 0 ? tasques.value[tasques.value.length - 1].id + 1 : 1
  tasques.value.push({ id: nouId, nom, completada: false })
}

const eliminarTasca = (id) => {
  tasques.value = tasques.value.filter(t => t.id !== id)
}

const marcarTasca = (id) => {
  const t = tasques.value.find(t => t.id === id)
  if (t) t.completada = !t.completada
}

const tasquesFiltrades = computed(() => {
  return mostrarPendents.value
    ? tasques.value.filter(t => !t.completada)
    : tasques.value
})

const totalTasques = computed(() => tasques.value.length)
const pendents = computed(() => tasques.value.filter(t => !t.completada).length)
</script>

<template>
  <div class="contenidor">
    <h1>Gestor de Tasques</h1>

    <!-- Formulari d'afegir tasca -->
    <TaskForm @afegir="afegirTasca" />

    <!-- Filtre -->
    <div class="filtre">
      <label>
        <input type="checkbox" v-model="mostrarPendents" />
        Mostra només pendents
      </label>
    </div>

    <!-- Llista de tasques -->
    <TaskList 
      :tasques="tasquesFiltrades" 
      @eliminar="eliminarTasca" 
      @marcar="marcarTasca" 
    />

    <!-- Resum -->
    <p class="resum">
      Total: {{ totalTasques }} | Pendents: {{ pendents }}
    </p>
  </div>
</template>


