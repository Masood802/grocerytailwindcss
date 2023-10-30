<template>
  <div class="p-2 bg-green-400 fixed w-full z-50">
    <Header></Header>
  </div>
  <div
    class="bg-center bg-cover w-full h-96 top-10 z-0 bg-fixed"
    style="background-image: url('public/main.jpg')"
  ></div>
  <div class="w-full">
    <h1 class="text-center text-red-500 text-3xl font-bold z-50">About Us</h1>
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Rerum, impedit
      ipsum illo hic minus nobis minima praesentium recusandae excepturi! Facere
      ad dolore voluptate minima, repellat sed corrupti sint, quos dolores quas
      consequuntur exercitationem incidunt perferendis error libero quidem earum
      voluptatum, veniam cupiditate doloribus saepe reprehenderit? Ad, fuga
      nemo. Inventore iste deleniti, fugit provident architecto, tenetur quas
      voluptatibus, dicta exercitationem vitae quia! Corrupti harum itaque,
      molestiae autem debitis dignissimos molestias repellat perspiciatis,
      voluptatum obcaecati voluptas nisi necessitatibus. Ullam odio minima quo
      fugit tempore voluptate iste. Repellendus id rem perferendis officia
      reprehenderit vel eos consectetur quasi enim, eligendi ratione, quae
      exercitationem magnam!
    </p>
  </div>
  <div class="absolute bg-slate-200 w-full py-5 top-[100%] bottom-10 flex justify-center items-center">
    <the-footer></the-footer>
  </div>
</template>
<script setup>
import { onMounted, ref } from "vue";
import Header from "../components/Header.vue";
import TheFooter from "../components/TheFooter.vue";
</script>

