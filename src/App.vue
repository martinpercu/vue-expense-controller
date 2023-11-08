<script setup>
// import Home from '@/components/Home.vue';
import Splashscreen from '@/components/splashscreen.vue';
import { defineAsyncComponent } from 'vue'

const Home = defineAsyncComponent(() => {
  return new Promise((resolve) => {
    console.log('in the promise charging in 1500');
    setTimeout(() => {
      console.log('charging now');
      resolve(import('@/components/Home.vue'))
    }, 1500);
  })
});

</script>

<template>
  <Suspense>
    <template #default>
      <Home></Home>
    </template>
    <template #fallback>
      <Splashscreen></Splashscreen>
    </template>
  </Suspense>
</template>

<style scoped>
html,
body,
.app {
  min-height: 100vh;
  margin: 0;
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}

/* * {
  --brand-blue: #3c70ab;
  --brand-green: #70ab3c;
} */
</style>
