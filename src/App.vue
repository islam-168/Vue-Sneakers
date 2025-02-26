<script setup>
// Base
import { onMounted, ref, watch } from 'vue'
import axios from 'axios'
// Components
import Header from '@/components/Header.vue'
import CardListVue from '@/components/CardList.vue'
import Drawer from '@/components/Drawer.vue'

const items = ref([])

const sortBy = ref('')
const searchQuery = ref('')

onMounted(async () => {
  try {
    const { data } = await axios.get('https://4169a22cf4a72ba8.mokky.dev/items')
    items.value = data
  } catch (error) {
    console.log(error)
  }
})

watch(sortBy, async () => { // watch следит за изменениями переменной `sortBy`
  try {
    const { data } = await axios.get('https://4169a22cf4a72ba8.mokky.dev/items?sortBy=' + sortBy.value)
    items.value = data
  } catch (error) {
    console.log(error)
  }
})

function sortItems(value) {
  sortBy.value = value
}
</script>

<template>
  <!--  <Drawer/>-->
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-8">
    <Header />

    <CardListVue :items="items" @changeSortBy="sortItems" />
  </div>
</template>
