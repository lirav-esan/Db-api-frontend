<template>
<div class="search-bar q-pa-sm">
    <input v-model="q" @input="onInput" placeholder="Buscar personaje por nombre..." class="search-input" />
</div>
</template>

<script>
import {
    ref
} from 'vue'
const emit = defineEmits(['search'])
const q = ref('')
let timer

function onInput() {
    clearTimeout(timer)
    timer = setTimeout(() => emit('search', q.value.trim()), 300)
}
</script>

<style scoped>
.search-input {
    width: 100%;
    padding: 8px 10px;
    border-radius: 6px;
    border: 1px solid #ccc
}
</style>
