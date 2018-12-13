<template>
  <div id="app">
    <select-grid :min-size="10" :columns="15" :rows="15"/>
  </div>
</template>

<script>
import SelectGrid from './components/SelectGrid.vue'

export default {
  name: 'app',
  components: {
    SelectGrid
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
