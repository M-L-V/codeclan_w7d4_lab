<template>
  <div id="app">
    <list-item></list-item>
  </div>
</template>

<script>
import ListItem from './components/ListItem'

export default {
  name: 'app',
  data() {
    return {
      energyMix: []
    }
  },
  mounted() {
    fetch("https://api.carbonintensity.org.uk/generation")
    .then(res => res.json())
    .then(respObject => {
      this.energyMix = respObject.data.generationmix
    })
  },
  components: {
    'list-item': ListItem
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
