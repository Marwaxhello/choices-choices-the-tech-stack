<script setup>
import HelloWorld from "./components/HelloWorld.vue";

import { ref, onMounted } from "vue";
import { request } from "./datocms";
const data = ref(null);
const error = ref(null);
const loading = ref(true);
const QUERY = `
{
  allArticles {
    title
  }
}`;

onMounted(async () => {
  try {
    data.value = await request({
      query: QUERY,
      variables: {
        limit: 10,
      },
    });
  } catch (e) {
    error.value = e;
  }
  loading.value = false;
});
</script>

<template>
  <main>
    <h1>MARWA</h1>
    <section v-if="loading">Loading...</section>
    <section v-else>
      {{ data.allArticles[1].title }}
    </section>
    <HelloWorld />
    <HelloWorld />
  </main>
</template>

<style scoped></style>
