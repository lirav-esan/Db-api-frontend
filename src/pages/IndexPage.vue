<template>
  <q-page class="q-pa-md">
    <div class="row items-start" style="gap: 20px">
      <div style="flex: 1">
        <h2>Dragon Ball Characters</h2>
        <CharacterList />
      </div>
    </div>
  </q-page>
</template>

<script setup>
import CharacterList from '@/components/dragonball/CharacterList.vue'
</script>

<style scoped>
h2 {
  margin: 0 0 8px;
}
</style>
