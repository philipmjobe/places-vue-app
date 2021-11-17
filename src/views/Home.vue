<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p>Place Name:</p>
    <input type="text" v-model="newPlaceParams.name" />
    <p>Address:</p>
    <input type="text" v-model="newPlaceParams.address" />
    <p></p>
    <ul>
      <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
    </ul>
    <p></p>
    <button v-on:click="createPlace()">Create Place</button>
    <div v-for="place in places" v-bind:key="place.id">
      <h2>{{ place.name }}</h2>
      <p>{{ place.address }}</p>
      <button v-on:clck="showPlace(place)">Update</button>
      <dialog id="place-details">
        <form method="dialog">
          <h2>Place Update</h2>
          <p>
            Name:
            <input type="text" v-model="currentPlace.name" />
          </p>
          <p>
            Address:
            <input type="text" v-model="currentPlace.address" />
          </p>
          <button v-on:click="updatePlace(currentPlace)">Update Place</button>
          <button v-on:click="destroyPlace(currentPlace)">Delete Place</button>
          <button>Close</button>
        </form>
      </dialog>
    </div>
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
