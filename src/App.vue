<template>
  <div id="app">
    <h1>Coding Test - Torre.co</h1>
    <button v-on:click="fetch">Find</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data: function () {
    return {
      information: []
    }
  },
  methods: {
    fetch() {
      //const headers = { "Content-Type": "application/json" };
      let result = axios
        .get("https://rickandmortyapi.com/api/character")
        .then(res => {
          this.information = res.data.results
          //console.log(res.data);
        })
        .catch(err => {
          console.log(err);
        })
      }
    } 
  };
</script>

