<template>
  <header class="text-white bg-color-secondary p-2">
    <div class="container h-100">
      <div class="row justify-content-between align-items-center h-100">
        <div class="col-auto">
          <div class="row align-items-center">
            <div class="col-auto">
              <img src="@/assets/img/logo.png" alt="logo" />
            </div>
            <div class="col-auto">
              <h1>Boolean Albums</h1>
            </div>
          </div>
        </div>
        <div class="col-auto">
          <div class="row align-items-center">
            <div class="col-auto">
              <h2>Genre:</h2>
            </div>
            <div class="col-auto">
              <select
                name="musicalGenre"
                id="musicalGenre"
                v-model="genreSelected"
                @change="getGenre"
              >
                <option value="All">All</option>
                <option
                  v-for="(genre, index) in genres"
                  :value="genre"
                  :key="index"
                >
                  {{ genre }}
                </option>
              </select>
            </div>
            <div class="col-auto">
              <h2>Artist:</h2>
            </div>
            <div class="col-auto">
              <select
                name="artist"
                id="artist"
                v-model="artistSelected"
                @change="getArtist"
              >
                <option value="All">All</option>
                <option
                  v-for="(artist, index) in artists"
                  :value="artist"
                  :key="index"
                >
                  {{ artist }}
                </option>
              </select>
            </div>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      genreSelected: "All",
      artistSelected: "All",
    };
  },
  props: ["albums"],
  methods: {
    getGenre() {
      this.$emit("getGenre", this.genreSelected);
    },
    getArtist() {
      this.$emit("getArtist", this.artistSelected);
    },
  },
  computed: {
    genres() {
      const genres = [];
      this.albums.forEach((album) => {
        if (!genres.includes(album.genre)) {
          genres.push(album.genre);
        }
      });
      return genres;
    },
    artists() {
      const artists = [];
      this.albums.forEach((album) => {
        if (!artists.includes(album.author)) {
          artists.push(album.author);
        }
      });
      return artists;
    },
  },
};
</script>

<style scoped lang="scss">
header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1;
  select {
    width: 175px;
    height: 50px;
    font-size: 18px;
  }
  img {
    height: 50px;
    vertical-align: middle;
  }
}
</style>
