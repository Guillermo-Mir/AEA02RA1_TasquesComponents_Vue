<script setup>
import { ref } from 'vue'

const novaTasca = ref('')

// definim l’event per comunicar al pare
const emit = defineEmits(['afegir'])

const enviar = () => {
  emit('afegir', novaTasca.value)
}
</script>

<template>
  <div class="nova-tasca">
    <input v-model="novaTasca" placeholder="Escriu una nova tasca" @keyup.enter="enviar"/>
    <button @click="enviar" class="btn-principal">Afegir</button>
  </div>
</template>
