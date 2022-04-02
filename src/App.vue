<script setup lang="ts">
import { ref } from "vue";
import { createApi } from "unsplash-js";
import SearchBox from "./components/SearchBox.vue";
import ImageLists from "./components/ImageLists.vue";

export type Photo = {
  id: number;
  width: number;
  height: number;
  urls: { large: string; regular: string; raw: string; small: string };
  color: string | null;
  user: {
    username: string;
    name: string;
  };
};

const inputRef = ref<Photo[]>([]);

const unsplash = createApi({
  accessKey: "Xx4O33YqvXp8q1O3yrtESRZUqzdvMtZn5qP0UsS_dFM",
});

const fetchApi = async (text: string) =>
  await unsplash.search
    .getPhotos({ query: text })
    .then((result) => {
      if (result.errors) {
        console.warn("error occurred: ", result.errors[0]);
      } else {
        console.log(result.response.results);
        //[todo]型が合わない
        // inputRef.value = result.response.results as Photo[];
        inputRef.value = result.response.results as any;
      }
    })
    .catch((e) => {
      console.error(e);
    });
const change = (text: string) => {
  fetchApi(text);
};
</script>

<template>
  <h2>Image Search</h2>
  <SearchBox @change="change" class="search-box" />
  <ImageLists :api="inputRef" v-if="Object.keys(inputRef).length" />
  <p v-else>nothing</p>
</template>

<style scoped>
.search-box {
  margin-bottom: 1em;
}
</style>
