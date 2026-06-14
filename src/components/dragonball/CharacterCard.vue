<template>
  <div class="character-card q-pa-sm">
    <div class="card-media">
      <img :src="character.image" :alt="character.name" />
    </div>
    <div class="card-body">
      <h3 class="name">{{ character.name }}</h3>
      <div class="meta">
        <span class="race">{{ character.race || 'Unknown' }},</span>
        <span class="aff">{{ character.affiliation || '—' }}</span>
      </div>
      <p class="desc">{{ descrip }}</p>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  character: {
    type: Object,
    required: true,
  },
})

const descrip = computed(() => {
  const d = props.character?.description
  if (!d) return 'No description available.'
  return d.length > 150 ? d.slice(0, 150) + '...' : d
})
</script>

<style scoped>
.character-card {
  display: flex;
  flex-direction: column;
  gap: 12px;
  align-items: flex-start;
  border: 1px solid #eee;
  border-radius: 8px;
  overflow: hidden;
}

.card-media img {
  width: 200px;
  height: 400px;
  object-fit: scale-down;
  display: block;
}

.card-body {
  padding: 8px 12px;
}

.name {
  margin: 0 0 6px;
  font-size: 1.1rem;
}

.meta {
  font-size: 0.85rem;
  color: #666;
  display: flex;
  gap: 8px;
  margin-bottom: 8px;
}

.desc {
  margin: 0;
  color: #444;
  font-size: 0.9rem;
}
</style>
