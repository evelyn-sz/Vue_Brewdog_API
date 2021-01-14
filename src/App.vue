<template lang="html">
  <div>
    <h1>Beer List</h1>
    <beers-list :beers="beers"></beers-list>
    <beer-detail :beer="selectedBeer"> </beer-detail>
    <ul>
      <h2 v-if="favouriteBeers[0]">Favourite beers</h2>
        <li v-for="favouriteBeer in favouriteBeers">{{ favouriteBeer.name }}
        <button type="submit" v-on:click="removeFromFavourites">Remove from favourites</button>
        </li>
    </ul>
  </div>
</template>

<script>
import {eventBus} from './main';
import BeersList from './components/BeersList.vue';
import BeerDetail from './components/BeerDetail.vue';
export default {
  // name: 'app',
  data() {
    return {
      beers: [],
      selectedBeer: null,
      favouriteBeers: [],
      favouriteBeer: {}
    }
  },
  mounted() {
    fetch('https://api.punkapi.com/v2/beers?page=1&per_page=80')
    .then(res => res.json())
    .then(beers => this.beers = beers);

    eventBus.$on('beer-selected', (beer) =>{
      this.selectedBeer = beer;

    }),
    eventBus.$on('beer-favourite', (beer) => {
      if (this.favouriteBeers.indexOf(beer) == -1)
      this.favouriteBeers.push(beer)
    })

  },
  methods: {
    removeFromFavourites (beer) {
      const index = this.favouriteBeers.indexOf(beer);
      this.favouriteBeers.splice(index);
    }
  },
  components: {
    "beers-list": BeersList,
    "beer-detail": BeerDetail,
    "beer-favourite": BeerDetail
  }
}

</script>

<style lang="css">
ul {
    list-style-type: none;
  }
</style>