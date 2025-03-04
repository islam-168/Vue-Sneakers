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
  try {
    if (!item.isFavorite) {
      const obj = {
        sneakerId: item.id,
      }
      const {data} = await axios.post('https://4169a22cf4a72ba8.mokky.dev/favorites', obj)

      item.isFavorite = true
      item.favoriteId = data.id
    } else {
      await axios.delete(`https://4169a22cf4a72ba8.mokky.dev/favorites/${item.favoriteId}`)

      item.isFavorite = false
      item.favoriteId = null
    }
  } catch (err) {
    console.log(err)
  }
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
      favoriteId: null,
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

    <CardList
      :items="items"
      @changeSortBy="sortItems"
      @changeSearchInput="searchItems"
      @addToFavorite="addToFavorite"
    />
  </div>
</template>
