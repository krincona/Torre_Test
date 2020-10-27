<template>
  <div class="column is-12-mobile is-4-desktop is-4-tablet">
    <div class="card">
      <div class="card-header">
        <img v-bind:src="user.image" v-bind:alt="user.name" />
      </div>
      <div class="card-content">
        <h3 class="title is-size-4">{{ user.name }}</h3>
        <button class="button is-rounded is-small is-info">More</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["user"],
};
</script>
