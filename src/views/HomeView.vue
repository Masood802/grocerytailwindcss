<script setup>
import { useRouter } from "vue-router";
import Header from "../components/Header.vue";
import TheFooter from "../components/TheFooter.vue";
let router = useRouter();
</script>

<template>
  <div
    class="z-50 fixed w-full p-2 bg-gradient-to-br from-green-500 to-yellow-400 shadow-md"
  >
    <Header></Header>
  </div>
  <div
    class="mx-auto w-full h-screen bg-cover bg-center top-16 absolute bg-fixed"
    style="background-image: url('public/background11.JPG')"
  >
    <div
      class="flex flex-col justify-center items-center absolute lg:top-64 lg:left-1/3 top-48 left-24"
    >
      <h1 class=" text-xl lg:text-3xl text-blue-800 font-bold">Welcome to Grocery Store</h1>
      <p class="text-sm lg:text-base">A place to find your fresh Grocery</p>
      <div>
        <button
          @click="router.push('/item-list')"
          class=" text-xs py-2 px-10 rounded text-slate-200 bg-green-950 my-2"
        >
          VISIT TO BUY
        </button>
      </div>
    </div>
  </div>
  <div class="absolute bg-slate-200 w-full py-5 top-[100%]">
    <the-footer></the-footer>
  </div>
</template>
