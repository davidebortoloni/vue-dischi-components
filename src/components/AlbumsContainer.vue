<template>
  <section id="album-container">
    <div
      v-for="(album, index) in filteredAlbums"
      :key="index"
      class="card bg-color-secondary"
    >
      <div>
        <img :src="album.poster" :alt="album.title" />
        <h2 class="title text-white">{{ album.title }}</h2>
      </div>
      <div class="text-grey">
        <address class="author text-medium">{{ album.author }}</address>
        <time :datetime="album.year" class="year text-small">{{
          album.year
        }}</time>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "AlbumsContainer",
  data() {
    return {};
  },
  props: ["albums", "genreSelected"],
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
      let filteredAlbums = sortedAlbums.slice();
      if (this.genreSelected !== "All") {
        filteredAlbums = sortedAlbums.filter(
          (album) => album.genre === this.genreSelected
        );
      }
      return filteredAlbums;
    },
  },
};
</script>

<style scoped lang="scss">
#album-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  .card {
    padding: 20px;
    margin: 20px;
    flex-basis: 200px;
    text-align: center;
    min-height: 375px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    img {
      width: 100%;
      height: auto;
    }
    .title {
      margin-top: 15px;
    }
  }
}
</style>
