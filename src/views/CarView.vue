<template>
<div class="container">
  <div v-if="car">
    <h1>The car id:{{route.params.id}}</h1>
    <p>Make: {{car.make}}</p>
    <p>Body: {{car.body}}</p>
    <p>Price: {{car.price}}</p>
    <p>Year: {{car.year}}</p>

    <div>
      <h2>Contact:</h2>
      <button @click="router.push(`/car/${route.params.id}/dealer`)" >Dealer</button>
      <button @click="router.push(`/car/${route.params.id}/manufacturer`)" >Manufacturer</button>
      <RouterView></RouterView>
    </div>


  </div>
  <div v-else>
    <h1>Car not found</h1>
  </div>

</div>
</template>

<script setup>
import {useRoute, useRouter} from "vue-router";
import {ref,onBeforeMount} from "vue";
import cars from "../data.json";

const router = useRouter()
const route = useRoute();
const car = ref(null);
const id = route.params.id;

onBeforeMount(() => {
  car.value = cars.find(c => c.id === parseInt(id));
})

</script>

<style scoped>

</style>