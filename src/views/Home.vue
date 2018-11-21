<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p v-for="place in places"> {{place.name}}</p>
    <p>name:<input type="text" v-model="newPlace.name"></p>
    <p>address:<input type="text" v-model="newPlace.address"></p>
    <button v-on:click="addPlace()">add a new place </button>
  </div>
</template>

<style>
</style>

<script>
var axios = require('axios');
export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      places: [],
      newPlace: {name: "", address: ""}
    };
  },
  created: function() {
    axios.get('http://localhost:3000/api/places').then(function(response) {
      console.log(response.data);
      this.places = response.data;     
    }.bind(this))
  },
  methods: {
    addPlace: function() {
      var params = {
        name: this.newPlace.name,
        address: this.newPlace.address
      };
      axios.post('http://localhost:3000/api/places', params).then(function(response) {
        console.log(response.data);
        this.places.push(response.data);
      }.bind(this))
      console.log('add the place');      
    }
  },
  computed: {}
};
</script>