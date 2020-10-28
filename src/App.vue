<template>
  <div id="app">
    <div class="hero is-dark is-bold m-4">
      <div class="hero-body">
        <div class="title"><span class="is-white">Users</span></div>
        <div class="subtitle"><span class="is-white">Skills</span></div>

        <div class="field has-addons is-pulled-right">
          <div class="control">
            <input
              v-model="search"
              type="text"
              class="input is-rounded"
              v-on:keyup.enter="searchData"
            />
          </div>
          <div class="control">
            <button class="button is-rounded is-info" v-on:click="searchData">
              Search
            </button>
          </div>
        </div>
      </div>
    </div>
    <span></span>
    <div class="container">
      <div
        class="columns is-desktop is-mobile is-tablet is-multiline is-centered"
      >
        <user @showModal="showModal" v-for="user of users" v-bind:key="user.id" v-bind:user="user" />
      </div>
    </div>
    <nav
      class="pagination is-centered"
      role="navegation"
      aria-label="pagination"
    >
      <a class="button pagination-previous" v-on:click="changePage(page - 1)"
        >Back</a
      >
      <ul class="pagination-list">
        <li>
          <a class="button pagination-link is-current">{{ page }}</a>
        </li>
      </ul>
      <a class="button pagination-next" v-on:click="changePage(page + 1)">
        Next</a
      >
    </nav>
  </div>
</template>

<script>
//<div >{{ user }}</div>
import axios from "axios";
import User from "./components/User";

export default {
  name: "App",
  components: {
    User, // user
  },
  data: function () {
    return {
      users: [],
      page: 1,
      pages: 1,
      search: "",
      modal:  false, 
      currentUser: {}
    };
  },
  create() {
    this.fetch();
  },
  methods: {  
    fetch() {
      const params = {
        page: this.page,
        name: this.search
      };
      let result = axios
        .get("https://rickandmortyapi.com/api/character/", { params })
        .then((res) => {
          this.users = res.data.results;
          //console.log(res.data.info);
          this.pages = res.data.info.pages;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    changePage(page) {
      this.page = page <= 0 || page > this.pages ? this.page : page;
      this.fetch();
    },
    searchData() {
      this.page = 1;
      this.fetch();
    },
    showModal(id) {
      this.fetchOne(id)
    },
    async fetchOne(id) {
      let result = await axios.get(`https://rickandmortyapi.com/api/character/${id}/`)
      this.currentUser = result.data  
      this.modal = true 
    }
  },
};
</script>

