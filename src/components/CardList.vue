<script setup>

import CardVue from './CardVue.vue'

const onClickAdd = () => {
  alert('clicked add card')
}
</script>

<template>
  <div class="p-10">
    <div class="flex justify-between items-center">
      <h2 class="text-3xl font-bold mb-8">Все кроссовки</h2>

      <div class="flex gap-5">
        <select class="py-1.5 px-3 border border-gray-300 rounded-md outline-none">
          <option>По названию</option>
          <option>По цене (сначала дешевые)</option>
          <option>По цене (сначала дорогие)</option>
          <option>По оценкам</option>
        </select>

        <div class="relative">
          <img class="absolute left-4 top-2.5" src="/search.svg" alt="Search"/>
          <input
            class="border border-gray-300 rounded-md py-1.5 pl-11 pr-4 outline-none focus:border-gray-500"
            type="text"
            placeholder="Поиск..."
          />
        </div>
      </div>
    </div>
    <div class="grid grid-cols-4 gap-5">
      <CardVue
        title="Мужские кроссовки New Blazer Mid Suede"
        imageUrl="/sneakers/sneakers-1.jpg"
        :price="40"
        :isFavorite="true"
        :isAdded="true"
        :onClickAdd="onClickAdd"
      />
      <CardVue title="Мужские кроссовки New Blazer Mid Suede" imageUrl="/sneakers/sneakers-1.jpg" :price="40"/>
      <CardVue title="Мужские кроссовки New Blazer Mid Suede" imageUrl="/sneakers/sneakers-1.jpg" :price="40"/>
      <CardVue title="Мужские кроссовки New Blazer Mid Suede" imageUrl="/sneakers/sneakers-1.jpg" :price="40"/>
      <CardVue title="Мужские кроссовки New Blazer Mid Suede" imageUrl="/sneakers/sneakers-1.jpg" :price="40"/>
      <CardVue title="Мужские кроссовки New Blazer Mid Suede" imageUrl="/sneakers/sneakers-1.jpg" :price="40"/>
      <CardVue title="Мужские кроссовки New Blazer Mid Suede" imageUrl="/sneakers/sneakers-1.jpg" :price="40"/>
    </div>
  </div>
</template>

<style scoped>

</style>
