<template>
  <div id="app">
    <div class="hero is-black is-bold">
      <div class="hero-body">
        <div class="title"><span class="is-white">Users</span></div>
        <div class="subtitle"><span class="is-white">Skills</span></div>
        <button class="button is-rounded is-info" v-on:click="fetch">
          Find
        </button>
      </div>
    </div>
    <span></span>
    <div class="container">
      <div class="columns is-desktop is-mobile is-tablet is-multiline is-centered">
        <user v-for="user of users" v-bind:key="user.id" v-bind:user="user" />
      </div>
    </div>
  </div>
</template>

<script>
//<div >{{ user }}</div>
import axios from "axios";
import User from "./components/User";

export default {
  name: "App",
  components: {
    User // user
  },
  data: function () {
    return {
      users: [],
    };
  },
  create() {
    this.fetch();
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

