<template>
  <div id="app">
    <header>
      <div class="container">
        <div>
          <img src="@/assets/img/logo.png" alt="logo" />
          <h1>Boolean Albums</h1>
        </div>
        <div>
          <h2>Filter:</h2>
          <select name="musicalGenre" id="musicalGenre" v-model="genreSelected">
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
      </div>
    </header>
    <main class="container">
      <section id="album-container">
        <div v-for="(album, index) in filteredAlbums" :key="index" class="card">
          <div>
            <img :src="album.poster" :alt="album.title" />
            <h2 class="title">{{ album.title }}</h2>
          </div>
          <div>
            <address class="author">{{ album.author }}</address>
            <time :datetime="album.year" class="year">{{ album.year }}</time>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      albums: [],
      genreSelected: "All",
    };
  },
  methods: {
    sortAlbums() {
      let sortedAlbums = this.albums.slice();
      sortedAlbums.sort(function(a, b) {
        return a.year - b.year;
      });
      console.log(this.albums);
      return sortedAlbums;
    },
  },
  computed: {
    filteredAlbums() {
      const sortedAlbums = this.sortAlbums();
      let filteredAlbums = sortedAlbums;
      if (this.genreSelected !== "All") {
        filteredAlbums = sortedAlbums.filter(
          (album) => album.genre === this.genreSelected
        );
      }
      return filteredAlbums;
    },
    genres() {
      const genres = [];
      this.albums.forEach((album) => {
        if (!genres.includes(album.genre)) {
          genres.push(album.genre);
        }
      });
      return genres;
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
/* Generals */

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  background-color: #1e2d3b;
  padding-top: 100px;
}

address {
  font-style: normal;
}

/* Utils  */

.container {
  max-width: 1200px;
  margin: 0 auto;
}

/* Header */

header {
  background-color: #2e3a46;
  height: 70px;
  padding: 10px;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
}
header .container {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
header select {
  width: 400px;
  height: 50px;
  font-size: 20px;
}
header h2,
header h1 {
  display: inline-block;
  color: white;
  margin: 0 20px;
  vertical-align: middle;
}

header img {
  height: 50px;
  vertical-align: middle;
}

/* Album */

#album-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

#album-container .card {
  background-color: #2e3a46;
  padding: 20px;
  margin: 20px;
  flex-basis: 200px;
  text-align: center;
  min-height: 375px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

#album-container .card img {
  width: 100%;
  height: auto;
}

#album-container .card .title {
  color: #fff;
  margin-top: 15px;
}
#album-container .card .author,
#album-container .card .year {
  color: #808080;
  font-size: 19px;
}
#album-container .card .year {
  font-size: 15px;
}
</style>
