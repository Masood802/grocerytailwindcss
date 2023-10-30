<template>
  <div
    class="z-50 fixed w-full p-3 bg-gradient-to-tr from-green-500 to-slate-300 top-0"
  >
    <Header></Header>
  </div>
  <h1 class="absoulte top-4 text-center lg:text-3xl mt-20 mb-5 font-bold text-xl">Cart</h1>
  <div
    class="w-11/12 mx-auto shadow-md shadow-slate-300 p-2"
    v-if="store.cartitems.length"
  >
    <div class=" flex justify-between items-center w-[99%] mx-auto my-2 bg-slate-50 px-3 box-border" v-for="record in store.cartitems" :key="record.id">
      <img :src="record.image" alt="ShowImage" class="lg:w-20 lg:h-20 w-12 h-12" />
      <h3 class="text-xs lg:text-base">{{ record.title }}</h3>
      <h4 class="text-xs lg:text-base">Price:{{ record.price }}/KG</h4>
      <h3 class="text-xs lg:text-base">quantity:{{ record.quantity }}</h3>
      <h4 class="text-xs lg:text-base">Total Price:{{ record.price * record.quantity }}</h4>
      <button @click="Delete(record.id)" class="bg-red-800 lg:px-5 py-1 text-xs px-2 text-slate-50">Delete</button>
    </div>
    <div class="flex justify-between items-center my-2 py-2 mx-auto w-[99%]">
      <h3 class="text-sm lg:text-base">Grand Total:{{ store.Gtotal }}</h3>
      <button
        v-if="store.cartitems.length > 0"
        @click="router.push('/checkout-form')"
        class="bg-green-700 lg:px-6 py-1 text-xs px-2 text-slate-50"
      >
        Checkout
      </button>
    </div>
  </div>
  <div class="Nocart" v-else>
    <p>There are no items in cart.....</p>
  </div>
  <div class="flex justify-center items-center my-4">
    <button @click="router.push('/item-list')" class="bg-green-700 lg:py-2 lg:px-4 text-sm py-1 px-2 text-slate-50 ">Add items to Cart</button>
  </div>
  <div class="bg-slate-200 w-full py-4 bottom-0 absolute lg:relative lg:bottom-0 ">
    <the-footer></the-footer>
  </div>
</template>

<script setup>
import { useRouter } from "vue-router";
import { useGroceryStore } from "../stores/grocery";
import Header from "../components/Header.vue";
import TheFooter from "../components/TheFooter.vue";
import { onMounted } from "vue";

let store = useGroceryStore();
let router = useRouter();
function Delete(id) {
  let delitem = store.cartitems.find((item) => item.id === id);
  if (delitem.quantity > 1) {
    delitem.quantity--;
    store.UpdateCart();
  } else {
    store.cartitems = store.cartitems.filter((item) => item.id != id);
    store.UpdateCart();
  }
}
</script>

<style scoped>

</style>
