<script setup>
import { computed, ref } from 'vue';

let photoGallery = ref([]);

const numberOfPhotos = computed(() => {
  return photoGallery.value.length;
});

const evenAlbums = computed(() => {
  return photoGallery.value.filter((item) => item.albumId % 2 === 0);
});

const oddAlbums = computed(() => {
  return photoGallery.value.filter((item) => !(item.albumId % 2 === 0));
});

const onlyAFewPics = computed(() => photoGallery.value.slice(0, 25));

function fetchPhotoGallery() {
  fetch('https://jsonplaceholder.typicode.com/photos')
    .then((response) => response.json())
    .then((json) => {
      photoGallery.value = json.slice(0, 25);
    });
}
</script>

<template>
  <main class="section">
    <section class="container">
      <h1 class="title">Photo Gallery</h1>
      <button @click="fetchPhotoGallery">Fetch Data</button>
      <p>
        {{ numberOfPhotos }} photos ({{ oddAlbums.length }} odd albums |
        {{ evenAlbums.length }} even albums)
      </p>
      <ul class="grid">
        <li
          class="cell"
          v-for="photo in onlyAFewPics"
          :key="`photo-id-${photo.id}`"
        >
          <img :src="photo.thumbnailUrl" />
        </li>
      </ul>
    </section>
  </main>
</template>

<style lang="scss">
@import './node_modules/bulma/bulma.sass';

.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
</style>
