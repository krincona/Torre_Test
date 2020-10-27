<template>
  <div id="app">
    <div class="hero is-primary is-bold ">
      <div class="hero-body">
        <div class="title"><span class="is-white">User</span></div>
        <div class="subtitle"><span class="is-white ">Skills</span></div>
        <button class="button is-rounded is-info " v-on:click="fetch">Find</button>
      </div>
    </div>

    <div class="container">
      <div class="columns is-desktop is-mobile is-tablet is-multiline is-centered">
        <div class="column is-12-mobile is-4-desktop is-4-tablet" v-for="user of users" v-bind:key="user.id"> 
          <div class="card">
            <div class="card-header"><img v-bind:src="user.image" v-bind:alt="user.name" /></div>
            <div class="card-content">
              <h3 class="title is-size-4">{{user.name}}</h3>
              <button class="button is-rounded is-small is-info">More</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>    
</template>

<script>
//<div >{{ user }}</div>
import axios from "axios";

export default {
  name: "App",
  data: function () {
    return {
      users: [],
    };
  },
  methods: {
    fetch() {
      //const headers = { "Content-Type": "application/json" };
      let result = axios
        .get("https://rickandmortyapi.com/api/character")
        .then((res) => {
          this.users = res.data.results;
          //console.log(res.data);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

