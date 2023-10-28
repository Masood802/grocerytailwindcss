<template>
  <div class="z-50 fixed w-full bg-gradient-to-tr from-green-500 to-slate-300 p-2 top-0">
    <Header></Header>
  </div>

  <h1 class="text-2xl text-green-950 font-semibold font-serif text-center my-4">
    list of items
  </h1>
  <div class="w-full flex flex-wrap justify-center mx-auto items-center">
    <div
      class="w-72 h-96 flex flex-col justify-center items-center mx-2 my-3 shadow-md rounded bg-white p-4 border border-gray-50"
      v-for="item in store.items"
      :key="item.id"
    >
      <img :src="item.image" alt="ShowImage" class="w-40 mx-2 my-3" />
      <h3 class="font-semibold font-serif">{{ item.title }}</h3>
      <h4 class="font-serif text-xs m-2">Price:{{ item.price }}/KG</h4>
      <p class="text-green-700 font-serif">{{ availabilty(item) }}</p>
      <button
        class="w-full bg-green-800 py-2 text-sm text-gray-50 my-1"
        @click="Additems(item)"
        :class="{ disabled: item.stock === 0 }"
        v-if="store.logedin"
      >
        Add to Cart
      </button>
      <button
        v-else
        @click="router.push('/sign-in')"
        class="w-full bg-green-800 py-2 text-sm text-gray-50 my-1"
      >
        Signin to add items
      </button>
      <button
        @click="buy(item)"
        :class="{ disabled: item.stock === 0 }"
        v-if="store.logedin"
        class="w-full bg-green-800 py-2 text-sm text-gray-50"
      >
        Buy
      </button>
    </div>
  </div>
  <div class="a bg-slate-200 w-full py-4 bottom-0">
<the-footer></the-footer>
  </div>
</template>
<script setup>
import { computed, onBeforeMount, onMounted, ref } from "vue";
import { useRouter } from "vue-router";
import { useGroceryStore } from "../stores/grocery";
import Header from "../components/Header.vue";
import TheFooter from "../components/TheFooter.vue";
import axios from "axios";
let router = useRouter();
let store = useGroceryStore();
function availabilty(item) {
  if (item.stock >= 10) return "Available";
  else if (item.stock < 10 && item.stock > 0) return "Low-Stock";
  else return "Not-Available";
}
onBeforeMount(async () => {
  const res = await axios.get("http://localhost:3000/items");
  store.items = await res.data;
});
function Additems(item) {
  let existingItem = store.cartitems.find((i) => i.id === item.id);
  if (existingItem) {
    existingItem.quantity++;
  } else {
    store.cartitems.push({ ...item, quantity: 1 });
  }
  store.UpdateCart();
}
function buy(item) {
  Additems(item);
  router.push("/checkout-form");
}
</script>
<style scoped>
.Not-Available,
.Low-Stock {
  color: red;
}
.disabled {
  background: rgb(200, 211, 195) !important;
  cursor: not-allowed !important;
}
</style>
