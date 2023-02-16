<template>
  <main>
    <div class="links">
      <RouterLink active-class="active" to="/">Home</RouterLink>
      <RouterLink active-class="active" to="/about">About</RouterLink>
    </div>
    <RouterView></RouterView>
  </main>
</template>

<script setup>
import {RouterView,RouterLink} from "vue-router";
</script>

<style scoped>
.links {
  padding: 20px
}
.links a {
  margin: 0 5px
}
.active {
  font-weight: bold;
}
</style>

