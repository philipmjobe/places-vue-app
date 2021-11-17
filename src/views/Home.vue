<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p>Place Name:</p>
    <input type="text" v-model="newPlaceParams.name" />
    <p>Address:</p>
    <input type="text" v-model="newPlaceParams.address" />
    <p></p>
  </div>
</template>

<style></style>

<script>
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
    };
  },
  created: function () {},
  methods: {},
};
</script>
