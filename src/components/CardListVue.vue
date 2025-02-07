<script setup>

import CardVue from './CardVue.vue'
</script>

<template>
  <div class="p-10">
    <h2 class="text-3xl font-bold mb-8">Все кроссовки</h2>

    <div class="grid grid-cols-4 gap-5">
      <CardVue
        title="Мужские кроссовки New Blazer Mid Suede"
        imageUrl="/sneakers/sneakers-1.jpg"
        :price="40"
        :isFavorite="true"
        :isAdded="true"
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
