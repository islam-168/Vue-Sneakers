<script setup>
import DrawerHead from "@/components/DrawerHead.vue";
import CartItemList from "@/components/CartItemList.vue";
</script>

<template>
  <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-75"></div>
  <div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-8">
    <DrawerHead />

    <CartItemList/>

    <div class="flex flex-col gap-4 my-4">
      <div class="flex gap-1">
        <span>Итого:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>1600 $</b>
      </div>

      <div class="flex gap-1">
        <span>Налог 5%:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>80 $</b>
      </div>

      <button
        disabled=""
        class="transition bg-lime-500 w-full rounded-md py-1 cursor-pointer text-white hover:bg-lime-600 active:bg-lime-700 disabled:bg-slate-300">
        Оформить заказ
      </button>
    </div>
  </div>
</template>

<style scoped>

</style>
