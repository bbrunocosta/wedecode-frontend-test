<template>
  <CnpjInput/>
</template>

<script>
import CnpjInput from './components/CnpjInput.vue'

export default {
  name: 'App',
  components: {
    CnpjInput
  }
}
</script>

<style>
html *{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
html,body, #app{
  height: 100vh;
  width: 100vw;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-image: linear-gradient(
      to top right,
      #ff8a00, #e52e71
    )
}
</style>
