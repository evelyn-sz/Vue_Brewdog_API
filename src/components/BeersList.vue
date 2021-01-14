<template lang="html">
    <!-- <div id="beersList"> -->
        <select  v-on:change="handleSelect" v-model="selectedBeer">
            <!-- <option v-for="(beer, index) in beers" :value="beer" :key="index"></option> -->
            <option v-for="beer in beers" :value="beer" >{{beer.name}}</option>
        </select>
    <!-- </div> -->
</template>

<script>

import {eventBus } from '../main.js'
export default {
    name: "beers-list",
    props: ["beers"],
    data() {
        return {
            "selectedBeer": {}         
        }
    },
    methods: {
        handleSelect() {
            eventBus.$emit('beer-selected', this.selectedBeer)
        }
    }

}
</script>

<style>

</style>