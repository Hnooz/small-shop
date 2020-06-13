<template>

  <div id="app">
    <Nav/>
   <Product/>
  </div>
</template>

<script>

import Nav from './components/Nav'
import Product from './components/Product'
export default {
  name: 'App',
  components:{
    Nav,
    Product,
  }
}
</script>

<style src="./assets/css/tailwind.css">

</style>




