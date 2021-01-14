<template lang="html">
    <div v-if='beer' id="beerDetail">
        <h2>Beer name: {{beer.name}}</h2>
            <div>
                <p><span>First brewed:</span>{{ beer.first_brewed }}</p>
                <button type="submit" id="button" v-on:click="addToFavourites">Add To Favourites</button>
            </div>
    </div>
</template>

<script>

import { eventBus } from '../main';
export default {
    name: "beer-detail",
    props: ['beer'],
    methods: {
        addToFavourites: function(){
            eventBus.$emit('beer-favourite', this.beer);
        }
    }

}
</script>

<style>

</style>