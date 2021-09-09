<template>
  <div
    id="album"
    class="bg-color-secondary p-3 h-100 d-flex flex-column justify-content-between"
  >
    <div>
      <img class="img-fluid" :src="album.poster" :alt="album.title" />
      <h4 class="title text-white mt-1">{{ album.title }}</h4>
    </div>
    <div class="text-grey p-3">
      <address class="author text-medium m-0">{{ album.author }}</address>
      <time :datetime="album.year" class="year text-small m-0">{{
        album.year
      }}</time>
    </div>
  </div>
</template>

<script>
export default {
  name: "Album",
  props: ["album"],
};
</script>
