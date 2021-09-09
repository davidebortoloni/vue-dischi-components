<template>
  <section id="album-container" class="row justify-content-center g-3">
    <div
      v-for="(album, index) in filteredAlbums"
      :key="index"
      class="col-2 text-center standard-height"
    >
      <Album :album="album" />
    </div>
  </section>
</template>

<script>
import Album from "./Album.vue";

export default {
  name: "AlbumsContainer",
  components: { Album },
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
.standard-height {
  min-height: 375px;
}
</style>
