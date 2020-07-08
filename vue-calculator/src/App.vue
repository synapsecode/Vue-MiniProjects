<template>
  <div id="app">
    <Calculator/>
   
  </div>
</template>

<script>
import Calculator from './components/AdvancedCalculator.vue'
export default {
  name: 'App',
  components: {
    Calculator
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body{
    background-image: url("https://exciteservices.net/images/bg-2.svg");
    background-size: 100%;
    
		background-color:rgb(24, 185, 97);
		background-blend-mode: multiply;
}
</style>
