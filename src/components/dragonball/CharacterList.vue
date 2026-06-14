<template>
<div class="character-list q-pa-md">
    <SearchBar @search="onSearch" />

    <div v-if="loading" class="q-mt-md">Cargando personajes...</div>

    <div v-else class="grid q-mt-md">
        <CharacterCard v-for="c in characters" :key="c.id" :character="c" />
    </div>

    <div v-if="error" class="error q-mt-md">{{ error }}</div>
</div>
</template>

<script>
import {
    ref,
    onMounted
} from 'vue'
import SearchBar from './SearchBar.vue'
import CharacterCard from './CharacterCard.vue'

const characters = ref([])
const loading = ref(false)
const error = ref(null)
const API = 'https://dragonball-api.com/api/characters'

async function fetchChars(query = '') {
    loading.value = true
    error.value = null
    try {
        const url = query ? `${API}?name=${encodeURIComponent(query)}` : API
        const res = await fetch(url)
        const data = await res.json()
        if (Array.isArray(data)) characters.value = data
        else if (data.items) characters.value = data.items
        else characters.value = []
    } catch (e) {
        print(e)
        error.value = 'No se pudo cargar la lista.'
    } finally {
        loading.value = false
    }
}

function onSearch(q) {
    fetchChars(q)
}

onMounted(() => fetchChars())
</script>

<style scoped>
.grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
    gap: 12px
}

.error {
    color: #c00
}
</style>
