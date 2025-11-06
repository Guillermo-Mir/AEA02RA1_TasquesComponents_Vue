<script setup>
import TaskItem from './TaskItem.vue'

// rebem la llista de tasques
const props = defineProps({
  tasques: Array
})

// events per passar al pare
const emit = defineEmits(['eliminar', 'marcar'])
</script>

<template>
  <ul class="llista-tasques">
    <TaskItem v-for="tasca in tasques" :key="tasca.id" :tasca="tasca" @eliminar="emit('eliminar', tasca.id)" @marcar="emit('marcar', tasca.id)"
    />
  </ul>
</template>
