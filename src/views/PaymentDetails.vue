<template>
  <div
    class="z-50 fixed w-full h-16 bg-gradient-to-br from-green-500 to-yellow-400 shadow-md"
  >
    <Header></Header>
  </div>
  <div
    class="w-full h-screen bg-cover blur-sm mx-1 bg-fixed z-0"
    style="background-image: url('public/background11.jpg')"
  ></div>
  <div class="w-1/2 absolute top-24 left-80 h-screen border leading-tight">
    <div
      class="h-60 rounded-lg bg-center bg-cover bg-no-repeat relativ w-[60%] mx-auto my-10"
      style="background-image: url('public/21.jpeg')"
    >
      <div class="flex justify-between items-center my-5 relative top-6">
        <img src="../assets/chip.png" alt="" class="w-16 ml-4 h-12" />
        <img src="../assets/visa.png" alt="visa" class="w-20 mx-4 h-12" />
      </div>
      <pre class="text-center text-xl font-bold mt-16">{{ cardNo }}</pre>
      <h3 class="absolute top-60 left-36 uppercase font-serif font-bold">
        {{ HolderName }}
      </h3>
      <h5 class="text-xs font-bold absolute left-40 top-52">
        VALID THRU {{ month }}/{{ year }}
      </h5>
    </div>
    <h1 class="text-xl font-bold text-center my-2">Payment Information</h1>
    <form @submit.prevent="Submit" class="w-[90%]">
      <div class="w-full flex justify-start items-center flex-col mx-auto">
        <label for="name" class="w-[80%] mx-auto text-slate-400 my-1"
          >Name on Card</label
        >
        <input
          type="text"
          name="name"
          v-model="HolderName"
          class="w-[80%] py-2 bg-transparent border border-slate-300 px-1 rounded"
        />
      </div>
      <div class="w-full flex justify-start items-center flex-col mx-auto">
        <label for="cardnum" class="w-[80%] mx-auto text-slate-400 my-1"
          >Card No</label
        >
        <input
          type="text"
          name="cardnum"
          v-model="cardNo"
          @input="updateCardNo"
          maxlength="16"
          class="w-[80%] py-2 bg-transparent border border-slate-300 px-1 rounded"
        />
      </div>
      <div class="flex flex-1 w-full">
        <div class="flex justify-between w-[90%] mr-1 flex-col">
          <span class="block pb-1 w-[80%]">Expiration MM</span>
          <select
            type="text"
            name="expiry"
            placeholder="Month"
            v-model="month"
            @keyup="updatemonth"
            id="month"
            class="w-[80%] p-2 border border-slate-400 rounded"
          >
            <option value="Month" selected>Month</option>
            <option value="1">1</option>
            <option value="2">2</option>
            <option value="3">3</option>
            <option value="4">4</option>
            <option value="5">5</option>
            <option value="6">6</option>
            <option value="7">7</option>
            <option value="8">8</option>
            <option value="9">9</option>
            <option value="10">10</option>
            <option value="11">11</option>
            <option value="12">12</option>
          </select>
        </div>
        <div class="flex justify-between w-[90%] flex-col">
          <span class="block pb-1 w-[80%]">Expiration YY</span>
          <select
            type="text"
            name="year"
            placeholder="year"
            v-model="year"
            @keyup="updateyear"
            id="year"
            class="w-[80%] p-2 border border-slate-400 rounded"
          >
            <option value="Year" selected>Year</option>
            <option value="2021">2021</option>
            <option value="2022">2022</option>
            <option value="2023">2023</option>
            <option value="2024">2024</option>
            <option value="2025">2025</option>
            <option value="2025">2025</option>
            <option value="2026">2026</option>
            <option value="2027">2027</option>
          </select>
        </div>
        <div class="flex justify-between w-[90%] flex-col">
          <span class="block pb-1 w-[80%]">CVC </span>
          <input
            type="text"
            name="CVC"
            placeholder="cvc"
            v-model="cvc"
            id="cvc"
            @input="updatecvc"
            maxlength="4"
            class="w-[80%] p-2 border border-slate-400 rounded"
          />
        </div>
      </div>

      <div class="gtotal">
        <p>Total Payment: {{ store.shipping + store.Gtotal }}</p>
      </div>
      <button @click="confirm">Confirm Payment</button>
    </form>
    <div class="paymentok" v-if="paymentdone">
      <p>Your Payment is Successful.check your account for ordertracking</p>
      <button @click="router.push('item-list')">Continue Shopping</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";
import Header from "../components/Header.vue";
import { useGroceryStore } from "../stores/grocery";
let store = useGroceryStore();
let cardNo = ref("1200 1400 1300 2100");
let HolderName = ref("MAsood UR Rehman");
let year = ref("2025");
let month = ref("12");
let cvc = ref("369");
let paymentdone = ref(false);
let router = useRouter();
function updateCardNo() {
  cardNo.value = document.getElementById("cardNo").value;
}
function updatemonth() {
  month.value = document.getElementById("month").value;
}
function updateyear() {
  year.value = document.getElementById("year").value;
}
function confirm() {
  if (
    cardNo.value === "" ||
    HolderName.value === "" ||
    month.value === "" ||
    year.value === ""
  ) {
    console.warn("Not-Valid Data");
    alert("Enter Valid data and try again");
  } else {
    paymentdone.value = true;
    store.orderDetail = store.cartitems;
    localStorage.setItem("order", JSON.stringify(store.orderDetail));
    localStorage.removeItem("cart");
    store.cartitems = [];
    cardNo.value = "XXXX XXXX XXXX XXXX";
    HolderName.value = "";
    month.value = "";
    year.value = "";
    store.shipping = 0;
  }
}
function updatecvc() {
  cvc.value = document.getElementById("cvc").value;
}
</script>
