<script setup>

import Card from './Card.vue'

defineProps({
  items: Array
})

const emit = defineEmits(['changeSortBy'], ['changeSearchInput'])

const onChangeSelectSort = (event) => {
  emit('changeSortBy', event.target.value);
}

const onChangeSearchInput = (event) => {
  emit('changeSearchInput', event.target.value);
}

const onClickAdd = () => {
  alert('clicked add card')
}
</script>

<template>
  <div class="p-10">
    <div class="flex justify-between items-center">
      <h2 class="text-3xl font-bold mb-8">Все кроссовки</h2>

      <div class="flex gap-5">
        <select @change="onChangeSelectSort" class="py-1.5 px-3 border border-gray-300 rounded-md outline-none">
          <option value="">По умолчанию</option>
          <option value="title">По названию</option>
          <option value="price">По цене (сначала дешевые)</option>
          <option value="-price">По цене (сначала дорогие)</option>
        </select>

        <div class="relative">
          <img class="absolute left-4 top-2.5" src="/search.svg" alt="Search"/>
          <input
            @input="onChangeSearchInput"
            class="border border-gray-300 rounded-md py-1.5 pl-11 pr-4 outline-none focus:border-gray-500"
            type="text"
            placeholder="Поиск..."
          />
        </div>
      </div>
    </div>
    <div class="grid grid-cols-4 gap-5">
      <Card
        v-for="(item, index) in items"
        :key="index"
        :title="item.title"
        :imageUrl="item.imageUrl"
        :price="item.price"
        :onClickAdd="onClickAdd"
      />
    </div>
  </div>
</template>

<style scoped>

</style>
