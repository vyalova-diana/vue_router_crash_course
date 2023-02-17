<script setup>
import carsData from "../data.json"
import {onMounted, ref, watch} from "vue";
import {useRoute, useRouter} from "vue-router";
const router = useRouter();
const route = useRoute();
const cars = ref(carsData);
const make = ref("All");

onMounted(() => {   //to share links with saved state
  if (route.query.make)
    make.value = route.query.make;

})

watch(route,() => {
  if (!route.query.make && make.value !==  "All")
    make.value = "All";
})


watch(make, () => {
    make.value === "All"  ? cars.value = carsData : cars.value = carsData.filter(c => c.make === make.value);
})
const handleChange = () => {
   router.push({query: {make: make.value}})
}
</script>

<template>
  <main class="container">
    <h1>Our Cars</h1>
    <select v-model="make" @change="handleChange">
      <option value="All">All</option>
      <option value="Chevrolet">Chevrolet</option>
      <option value="Buick">Buick</option>
      <option value="Porsche">Porsche</option>
      <option value="Audi">Audi</option>
    </select>
    <div class="cards">
      <div @click="router.push(`/car/${car.id}`)" v-for="car in cars" :key="car.id" class="card">
        <h1>{{car.make}}</h1>
        <p>${{car.price}}</p>
      </div>
    </div>
  </main>
</template>

<style scoped>
.cards {
  margin-top: 50px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 15px 20px;
}
.card {
  box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.207);
  padding: 15px;
  width: 150px;
  cursor: pointer;
}

</style>