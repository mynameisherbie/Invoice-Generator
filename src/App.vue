<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <InvoiceForm></InvoiceForm>
  </div>
</template>

<script>
import InvoiceForm from './components/InvoiceForm.vue'

export default {
  name: 'App',
  components: {
    InvoiceForm
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
  background-color: papayawhip;
}
</style>
