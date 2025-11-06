<script setup>
// rebem cada tasca com a prop
const props = defineProps({
  tasca: Object
})

// definim events per avisar al pare
const emit = defineEmits(['eliminar', 'marcar'])
</script>

<template>
  <li :class="{ completada: tasca.completada }">
    <div class="tasca-text">
      {{ tasca.nom }}
    </div>
    <div class="accions">
      <button @click="emit('marcar')" class="btn btn-secundari">
        {{ tasca.completada ? 'Desmarcar' : 'Completar' }}
      </button>
      <button @click="emit('eliminar')" class="btn btn-eliminar">
        🗑️
      </button>
    </div>
  </li>
</template>

<style scoped>
.completada {
  text-decoration: line-through;
  color: gray;
}
</style>
