<template>
  <div
    class="z-50 fixed w-full p-3 bg-gradient-to-tr from-green-500 to-slate-300 top-0"
  >
    <Header></Header>
  </div>
  <h1 class="absoulte top-4 text-center text-3xl mt-20 mb-5 font-bold">Cart</h1>
  <div
    class="w-11/12 mx-auto shadow-md shadow-slate-300 p-2"
    v-if="store.cartitems.length"
  >
    <div class=" flex justify-between items-center w-[99%] mx-auto my-2 bg-slate-50 px-3 box-border" v-for="record in store.cartitems" :key="record.id">
      <img :src="record.image" alt="ShowImage" class="w-20  h-20" />
      <h3>{{ record.title }}</h3>
      <h4>Price:{{ record.price }}/KG</h4>
      <h3>quantity:{{ record.quantity }}</h3>
      <h4>Total Price:{{ record.price * record.quantity }}</h4>
      <button @click="Delete(record.id)" class="bg-red-800 text-sm px-5 py-1 text-slate-50">Delete</button>
    </div>
    <div class="flex justify-between items-center my-2 py-2 mx-auto w-[99%]">
      <h3>Grand Total:{{ store.Gtotal }}</h3>
      <button
        v-if="store.cartitems.length > 0"
        @click="router.push('/checkout-form')"
        class="bg-green-700 px-6 py-1 text-slate-50"
      >
        Checkout
      </button>
    </div>
  </div>
  <div class="Nocart" v-else>
    <p>There are no items in cart.....</p>
  </div>
  <div class="flex justify-center items-center my-4">
    <button @click="router.push('/item-list')" class="bg-green-700 py-2 px-4 text-slate-50 ">Add items to Cart</button>
  </div>
  <div class="bg-slate-200 w-full py-4 bottom-0">
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
