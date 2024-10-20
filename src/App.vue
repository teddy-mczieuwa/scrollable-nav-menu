<template>
  <div class="bg-green-50 h-screen md:h-none overflow-y-scroll mt-2 md:mt-0">
    <section class="mt-4 md:mt-4 md:w-full bg-green-50 md:overflow-y-scroll">
      <div class="rounded-lg md:overflow-y-scroll">
        <h3 class="text-2xl text-green-800 mb-3 md:text-left text-center">
          Scrollable Nav Menu
        </h3>

        <div
          class="mx-auto rounded-lg md:border-0 border-green-800 md:py-8 mt-16 md:mt-10 mb-8 md:mb-2 h-96 flex justify-center items-center w-full"
        >
          <scrollable-nav-menu
            :list="list"
            v-model:item="item"
            :scrollDistance="400"
          />
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import ScrollableNavMenu from "./components/ScrollableNavMenu.vue";

const item = ref("");
const list = ref([
  "html",
  "react",
  "coding",
  "sql",
  "mongoDB",
  "news",
  "node.js",
  "css",
  "databases",
  "programming",
  "vue",
  "graphics",
  "redis",
  "devops",
  "AWS",
  "javascript",
  "angular",
  "editing",
]);
</script>
