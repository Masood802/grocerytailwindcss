<template>
  <div class="w-full m-auto flex justify-between items-center h-12">
    <div class="w-1/4 flex justify-between items-center">
      <div
        class="flex flex-col items-center mt-3 ml-2 text-blue-800 leading-tight"
        @click="router.push('/')"
      >
        <img src="../assets/grocery.png" class="w-6 h-6" />
        Grocery <span class="text-red-700 z-50">Store</span>
      </div>
      <router-link :to="{ path: '/' }" class="text-lime-800">
        Home
      </router-link>
      <router-link :to="{ path: '/item-list' }" class="text-lime-800">
        Item-List
      </router-link>
      <router-link :to="{ path: '/cart' }" class="text-lime-800">
        Cart
        <sup class="text-red-700 font-semibold text-base">{{
          store.totalitems
        }}</sup>
      </router-link>
      <router-link :to="{ path: '/about' }" class="text-lime-800">
        About
      </router-link>
    </div>
    <div class="text-green-900">
      <router-link :to="{ path: '/sign-in' }" class="m-4 text-green-900"
        ><span v-if="store.logedin === false">Signin</span
        ><span v-else @click="show"
          >Welcome {{ store.user.firstName }}</span
        ></router-link
      >
      <div v-if="toggleshow && store.logedin">
        <button
          @click="store.signout()"
          class="w-20 bg-green-900 text-slate-100 text-sm rounded my-2"
        >
          Signout
        </button>
        <button
          @click="router.push('/profile')"
          class="w-20 bg-green-900 text-slate-100 text-sm rounded ml-2"
        >
          Profile
        </button>
      </div>
      <router-link
        :to="{ path: '/registration-form' }"
        v-if="store.logedin === false"
        >Signup</router-link
      >
    </div>
  </div>
</template>

<script setup>
import { RouterLink, useRouter } from "vue-router";
import { useGroceryStore } from "../stores/grocery";
import { ref } from "vue";
let store = useGroceryStore();
let router = useRouter();
let toggleshow = ref();
function show() {
  toggleshow.value = !toggleshow.value;
  console.log(toggleshow.value);
}
</script>
