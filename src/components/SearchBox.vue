<script setup lang="ts">
import { ref } from "vue";

const emit = defineEmits<{ (event: "change", value: string): void }>();
const input = ref<string>("");

const handleEnter = () => {
  emit("change", input.value);
};
</script>

<template>
  <input type="text" v-model="input" @keypress.enter="handleEnter" />
</template>
