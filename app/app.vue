<script>
import { defineNuxtComponent } from '#app';

export default defineNuxtComponent({
  data: () => ({
    photoList: [],
  }),
  methods: {
    fetchPhotoList() {
      fetch('https://jsonplaceholder.typicode.com/photos/')
        .then((res) => res.json())
        .then((json) => {
          this.photoList = json;
        });
    },
  },
});
</script>

<template>
  <div>
    <h1>Photo Gallery</h1>
    <button @click="fetchPhotoList">Get Photos</button>
    <!-- <pre>{{ photoList }}</pre> -->
    <ul>
      <li v-for="photo in photoList" :key="`photo-id-${photo.id}`">
        <img :src="photo.thumbnailUrl" alt="" />
      </li>
    </ul>
  </div>
</template>

<style>
ul {
  list-style-type: none;
}
</style>
