<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p>Place Name:</p>
    <input type="string" v-model="newPlaceParams.name" />
    <p>Address:</p>
    <input type="string" v-model="newPlaceParams.address" />
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
const axios = require("axios");


export default {
  data: function () {
    return {
      message: "So many places!",
      places: [],
      newPlaceParams: {},
      currentPlace: {},
      errors: [],
    };
  },
  created: function () {
    this.indexPlaces();
  },
 indexPlaces: function () {
      axios
        .get("http://localhost:3000/places")
        .then((response) => {
          this.places = response.data;
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    createPlace: function () {
      axios
        .post("http://localhost:3000/places", this.newPlaceParams)
        .then((response) => {
          console.log(response.data);
          this.places.push(response.data);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    showPlace: function (place) {
      this.currentPlace = place;
      console.log(place);
      document.querySelector("#place-details").showModal();
    },
    updatePlace: function (place) {
      axios
        .patch("http://localhost:3000/places/" + place.id, place)
        .then((response) => {
          console.log("Place Created", response.data);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    destroyPlace: function (place) {
      axios
        .delete("http://localhost:3000/places/" + place.id)
        .then((response) => {
          console.log("Place Destroyed", response.data);
          var index = this.places.indexOf(place);
          this.places.splice(index, 1);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
