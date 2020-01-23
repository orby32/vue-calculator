<template>
  <div class="container" id="app">
    <h1>Vue Calculator</h1>
    <app-calculator></app-calculator>
  </div>
</template>

<script>
import Calculator from './Calculator.vue';
export default {
  components: {
    'app-calculator': Calculator
  }
}
</script>

<style>

</style>
