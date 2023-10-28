<template>
  <div
    class="w-full p-3 bg-gradient-to-bl from-green-500 to-yellow-400 shadow-md fixed top-0 z-50"
  >
    <Header></Header>
  </div>
  <div
    class="w-full h-screen bg-cover blur-sm mx-1 bg-fixed z-0"
    style="background-image: url('public/background11.jpg')"
  ></div>

  <div
    class="text-xl font-bold absolute top-96 left-96"
    v-if="store.logedin === false"
  >
    <h1>
      You are not loged in please
      <router-link
        :to="{ path: '/sign-in' }"
        class="decoration-red-700 underline text-blue-700"
        >Signin
      </router-link>
      or
      <router-link
        :to="{ path: '/registration-form' }"
        class="decoration-red-700 underline text-blue-700"
        >Signup </router-link
      >here
    </h1>
  </div>
  <div class="absolute top-20 w-[80%] mx-auto left-32" v-else>
    <h1 class="text-xl mx-auto text-center my-3">
      ----------Your Order Summry---------
    </h1>
    <ul class="grid grid-flow-col grid-cols-5 w-[80%] mx-auto">
      <li
        class="border border-gray-500 border-solid py-2 text-center"
      >
        Serial No
      </li>
      <li
        class="border border-gray-500 border-solid py-2 text-center "
      >
        Name
      </li>
      <li
        class="border border-gray-500 border-solid py-2 text-center"
      >
        Price
      </li>
      <li
        class="border border-gray-500 border-solid py-2 text-center"
      >
        quantity
      </li>
      <li
        class="border border-gray-500 border-solid py-2 text-center"
      >
        Total Price
      </li>
    </ul>
    <ul
      v-for="(record, index) in store.cartitems"
      :key="record.id"
      class="grid grid-flow-col grid-cols-5 w-[80%] mx-auto"
    >
      <li class="border border-gray-500 border-solid py-2 text-center">{{ index + 1 }}</li>
      <li class="border border-gray-500 border-solid py-2 text-center">{{ record.title }}</li>
      <li class="border border-gray-500 border-solid py-2 text-center">{{ record.price }}</li>
      <li class="border border-gray-500 border-solid py-2 text-center">{{ record.quantity }}</li>
      <li class="border border-gray-500 border-solid py-2 text-center">{{ record.price * record.quantity }}</li>
    </ul>
    <ul class="grid grid-flow-col grid-cols-5 mx-auto w-[80%]">
      <li class="border border-gray-500 border-solid py-2 text-center col-span-4">Total</li>
      <li class="border border-gray-500 border-solid py-2 text-center">{{ store.Gtotal }}</li>
    </ul>
    <ul class="grid grid-flow-col grid-cols-5 mx-auto w-[80%]">
      <li class="border border-gray-500 border-solid py-2 text-center col-span-4">Shipping Fee</li>
      <li  class="border border-gray-500 border-solid py-2 text-center">{{ store.shipping }}</li>
    </ul>
    <ul class="grid grid-flow-col grid-cols-5 mx-auto w-[80%]">
      <li class="border border-gray-500 border-solid py-2 text-center col-span-4">Grand Total</li>
      <li class="border border-gray-500 border-solid py-2 text-center">{{ store.shipping + store.Gtotal }}</li>
    </ul>
    <button @click="router.push('/payment-details')" class="w-[79%] bg-green-700 py-2 my-2 left-28 absolute rounded text-gray-50">
      Add payment Details to confirm order
    </button>
  </div>
  
</template>

<script setup>
import { useGroceryStore } from "../stores/grocery";
import Header from "../components/Header.vue";
import { onMounted } from "vue";
import { useRouter } from "vue-router";

let store = useGroceryStore();
let router = useRouter();
onMounted(() => {
  store.calculateshipping();
});
</script>

<style scoped>

</style>
