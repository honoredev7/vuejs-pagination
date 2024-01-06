<script setup>
import Pagination from './components/Pagination.vue'
import { ref, computed } from 'vue'

const items = ref([0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14])
const itemsPerPage = ref(5)
const currentPage = ref(1)

const totalItems = computed(() => items.value.length)

const totalPages = computed(() => Math.ceil(totalItems.value / itemsPerPage.value))

const currentItems = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage.value
  const end = start + itemsPerPage.value
  return items.value.slice(start, end)
})

const previousPage = () => {
  currentPage.value = currentPage.value - 1
}
    
const nextPage = () => {
  currentPage.value = currentPage.value + 1
}
</script>

<template>
  <div>
    <ul>
      <li v-for="(item, i) in currentItems" :key="i">{{ item }}</li>
    </ul>

    <div class="pagination">
      <button @click="previousPage" :disabled="currentPage === 1">Précédent</button>
      <span>{{ currentPage }} / {{ totalPages }}</span>
      <button @click="nextPage" :disabled="currentPage === totalPages">Suivant</button>
    </div>
  </div>
</template>

<style scoped>
ul li {
  list-style: none;
}
</style>
