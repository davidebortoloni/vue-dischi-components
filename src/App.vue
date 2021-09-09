<template>
  <div id="app">
    <div v-if="isLoading">
      <Loader />
    </div>
    <div v-else>
      <Header :albums="albums" @getGenre="getGenre" @getArtist="getArtist" />
      <main class="container">
        <AlbumsContainer
          :albums="albums"
          :genreSelected="genreSelected"
          :artistSelected="artistSelected"
        />
      </main>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Header from "./components/Header.vue";
import Loader from "./components/Loader.vue";
import AlbumsContainer from "./components/AlbumsContainer.vue";

export default {
  name: "App",
  components: { Header, AlbumsContainer, Loader },
  data() {
    return {
      albums: [],
      genreSelected: "All",
      artistSelected: "All",
      isLoading: true,
    };
  },
  methods: {
    getGenre(genre) {
      this.genreSelected = genre;
    },
    getArtist(artist) {
      this.artistSelected = artist;
    },
  },
  created() {
    axios
      .get("https://flynn.boolean.careers/exercises/api/array/music")
      .then((res) => {
        this.albums = res.data.response;
        this.isLoading = false;
      });
  },
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
@import "./assets/scss/style.scss";
</style>
