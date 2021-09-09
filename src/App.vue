<template>
  <div id="app">
    <Header :albums="albums" @getGenre="getGenre" />
    <main class="container">
      <AlbumsContainer :albums="albums" :genreSelected="genreSelected" />
    </main>
  </div>
</template>

<script>
import axios from "axios";
import AlbumsContainer from "./components/AlbumsContainer.vue";
import Header from "./components/Header.vue";

export default {
  name: "App",
  components: { Header, AlbumsContainer },
  data() {
    return {
      albums: [],
      genreSelected: "All",
    };
  },
  methods: {
    getGenre(genre) {
      this.genreSelected = genre;
    },
  },
  created() {
    axios
      .get("https://flynn.boolean.careers/exercises/api/array/music")
      .then((res) => {
        this.albums = res.data.response;
      });
  },
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
@import "@/assets/scss/style.scss";
</style>
