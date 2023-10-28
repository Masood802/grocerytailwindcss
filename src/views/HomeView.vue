<script setup>
import { useRouter } from "vue-router";
import Header from "../components/Header.vue";
import TheFooter from "../components/TheFooter.vue";
let router = useRouter();
</script>

<template>
  <div class="z-50 fixed w-full p-3 bg-gradient-to-br from-green-500 to-yellow-400 shadow-md"><Header></Header></div>
  <div class="w-full m-auto h-2/3">
    <img
      src="../assets/background11.JPG"
      alt="image"
      class="w-full z-0 h-screen overflow-hidden top-3 absolute"
    />
    <div
      class="flex flex-col justify-center items-center absolute top-64 left-1/3"
    >
      <h1 class="text-3xl text-blue-800 font-bold">Welcome to Grocery Store</h1>
      <p>A place to find your fresh Grocery</p>
      <div class="button">
        <button
          @click="router.push('/item-list')"
          class="py-2 px-10 rounded text-slate-200 bg-green-950 my-2"
        >
          VISIT TO BUY
        </button>
      </div>
    </div>
  </div>
  <div class="absolute bg-slate-200 w-full py-4 bottom-0">
<the-footer></the-footer>
  </div>
</template>
