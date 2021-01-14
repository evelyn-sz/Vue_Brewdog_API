<template>
  <div>
    <h1>Beer List</h1>
    <beers-list :beers="beers"></beers-list>
  </div>
</template>

<script>
import {eventBus} from './main';
import BeersList from './components/BeersList.vue';
export default {
  // name: 'app',
  data() {
    return {
      beers: [],
      selectedBeer: null
    }
  },
  mounted() {
    fetch('https://api.punkapi.com/v2/beers')
    .then(res => res.json())
    .then(beers => this.beers = beers);

    eventBus.$on('beer-selected', (beer) =>{
      this.selectedBeer = beer;
    })
  },
  components: {
    "beers-list": BeersList
  }
}

</script>

<style>

</style>