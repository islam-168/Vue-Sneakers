<script setup>
// Base
import { onMounted, reactive, ref, watch } from 'vue'
import axios from 'axios'
// Components
import Header from '@/components/Header.vue'
import CardList from '@/components/CardList.vue'
import Drawer from '@/components/Drawer.vue'

const items = ref([])

const filters = reactive({
  sortBy: '',
  searchQuery: ''
})

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get('https://4169a22cf4a72ba8.mokky.dev/favorites')
    // data: favorites - переименования свойства data из axios в favorites
    items.value = items.value.map(item => {
      const favorite = favorites.find((favorite) => favorite.sneakerId === item.id)

      if (!favorite) return item

      return {
        ...item,
        isFavorite: true,
        favoriteId: favorite.id
      }
    })
  } catch (error) {
    console.log(error)
  }
}

const addToFavorite = async (item) => {
  item.isFavorite = true
}

const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy
    }

    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`
    }

    const { data } = await axios.get(
      'https://4169a22cf4a72ba8.mokky.dev/items',
      {
        params,
      }
    )
    items.value = data.map((item) => ({
      ...item,
      isFavorite: false,
      isAdded: false,
    }))
  } catch (error) {
    console.log(error)
  }
}

onMounted(async () => {
  await fetchItems()
  await fetchFavorites()
})
watch(filters, fetchItems)

function sortItems(value) {
  filters.sortBy = value
}

function searchItems(value) {
  filters.searchQuery = value
}
</script>

<template>
  <!--  <Drawer/>-->
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-8">
    <Header />

    <CardList :items="items" @changeSortBy="sortItems" @changeSearchInput="searchItems" />
  </div>
</template>
