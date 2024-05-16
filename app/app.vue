<script setup>
import { computed, ref } from 'vue';
import PhotoGallery from './components/PhotoGallery.vue';
import TodoViewer from './components/TodoViewer.vue';

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
  <main class="container">
    <section class="section">
      <div class="columns">
        <div class="column">
          <PhotoGallery />
        </div>
        <div class="column">
          <TodoViewer title="new title" />
        </div>
      </div>
    </section>
  </main>
</template>

<style lang="scss">
@import './node_modules/bulma/bulma.sass';
@import './assets/styles/main.scss';
</style>
