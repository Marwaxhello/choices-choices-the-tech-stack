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
   <h1>Visual Thinking</h1>
   
    <section v-if="loading">Loading...</section>
    <section v-else>
      {{ data.allArticles[0].title }}
    </section>


    <div class="">
    <section class="video-arrows">
      <button class="arrows">
        <img
          class="left-arrow"
          src="./assets/pijl-hexagon-naar-beneden.svg"
          alt="Knop met pijl naar volgende video"
        />
      </button>
    </section>
    </div>

  
      <iframe class="ytp-cued-thumbnail-overlay-image"
      width="560"
      height="315"
      src="https://www.youtube.com/embed/yr-rRMElLFg?si=CkdyjnxpUFMqM7se"
      title="YouTube video player"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
      allowfullscreen
    />

      <div class="beschrijving">
      <h3 class="youtube-video-naam">
        Visual thinking in het hbo: onderzoeken en begrijpen
      </h3>

      <p>
        Deze kennisclip gaat over visual thinking en hoe het kan worden
        toegepast om zowel studenten als docenten in het hbo op een andere
        manier te leren onderzoeken.
      </p>

      <br />

      <p>
        Deze kennisclips zijn onderdeel van het platform ‘Visual thinking in het
        hbo’. Dit platform staat vanaf 2024 online. Tot die tijd kunnen
        werkvormen opgevraagd worden bij Charley Muhren, docent en onderzoeker
        bij CMD Amsterdam: c.j.muhren@hva.nl.
      </p>
    

       <section class="video-arrows">
      <button class="arrows">
        <img
          class="right-arrow"
          src="./assets/pijl-hexagon-naar-beneden.svg"
          alt="Knop met pijl naar volgende video"
        />
      </button>
    </section>

    </div>
    <HelloWorld />
  </main>
</template>

<style scoped>

  /* Iframe styling */

  .ytp-cued-thumbnail-overlay-image {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 2em;
    margin-top: 2em;
  }

  .video-arrows {
    margin: 1em;
  }

   /* Arrow buttons */
 .arrows {
    width: 72px;
    height: 66px;
    border: none;
    background: var(--vtYellow);
  }

  .right-arrow {
    transform: rotate(270deg);
  }

  .left-arrow {
    transform: rotate(90deg);
  }

.beschrijving {
    max-width: 500px;
    max-height: 409px;
    margin-left: 1em;
  }

</style>
