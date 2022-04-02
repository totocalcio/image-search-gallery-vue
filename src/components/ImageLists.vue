<script setup lang="ts">
import type { Photo } from "../App.vue";

type Props = {
  api: Photo[];
};

defineProps<Props>();
</script>

<template>
  <div class="grid">
    <figure v-for="item in api" :key="item.id">
      <img :src="item.urls.small" alt="" />
    </figure>
  </div>
</template>

<style scoped>
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 10px;
}
figure {
  object-fit: cover;
  margin: 0;
}
img {
  width: 100%;
}
</style>
