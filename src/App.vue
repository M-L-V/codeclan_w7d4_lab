<template>
  <div id="app">
    <h1>Energy Mix UK</h1>
    <fuel-chart :childEnergyMix="list" v-if="list"></fuel-chart>
    <list-item v-bind:childEnergyMix="list" :fromDate="fromDate" :toDate="toDate" v-if="list"></list-item>
    <date-form></date-form>
  </div>
</template>

<script>
import ListItem from './components/ListItem';
import FuelChart from './components/FuelChart';
import DateForm from './components/DateForm';
import { eventBus } from './main';

export default {
  name: 'app',
  data() {
    return {
      energyMix: [],
      fromDate: "",
      toDate: "",
      inputFromDate: "",
      inputToDate: ""
    }
  },
  computed: {
    list: function() {
      if (this.inputFromDate != "" && this.inputToDate != "") {
        const url = "https://api.carbonintensity.org.uk/generation/"+this.inputFromDate+"Z/"+this.inputToDate+"Z"
        let list = [];
        fetch(url)
          .then(res => res.json())
          .then(respObject => list = respObject.data[0].generationmix.map(fuelObj => Object.values(fuelObj)));
        return list;
      }
      return this.energyMix;
    }
  },
  mounted() {
    fetch("https://api.carbonintensity.org.uk/generation")
    .then(res => res.json())
    .then(respObject => {
      this.energyMix = respObject.data.generationmix.map(fuelObj => Object.values(fuelObj));
      this.energyMix.unshift(['fuel', 'percentage']);
      this.fromDate = respObject.data.from;
      this.toDate = respObject.data.to;
    });

    eventBus.$on("input-from-date", date => this.inputFromDate = date);
    eventBus.$on("input-to-date", date => this.inputToDate = date);
  },
  components: {
    'list-item': ListItem,
    'fuel-chart': FuelChart,
    'date-form': DateForm
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
