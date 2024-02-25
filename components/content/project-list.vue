
<template>
  <div class="not-prose">
    <section v-if="pending">loading ...</section>
    <section v-else-if="error">something went wrong ...</section>
    <section v-else>
      <ul class="grid grid-cols-1 gap-4">
        <li
          v-for="repo in repos"
          :key="repo.id"
          class="border border-gray-200 dark:border-gray-800 rounded-sm p-4 hover:bg-gray-200 dark:hover:bg-gray-800 font-mono"
        >
          <a
            :href="repo.html_url"
            target="_blank"
          >
            <div class="flex items-center justify-between">
              <div class="font-semibold">{{ repo.name }}</div>
              <div>
                {{ repo.stargazers_count }} ★
              </div>
            </div>
            <p class="text.sm">
              {{ repo.description }}
            </p>
          </a>

        </li>
      </ul>
    </section>
  </div>
</template>

<script setup>
/* 
imports
*/
import { computed } from 'vue'

/* 
fetch repos
*/
const { error, pending, data } = await useFetch('https://api.github.com/users/hoang227/repos')

/*
sort repos
*/
const repos = computed( // filter out repos with description then sort them
  () => data.value.filter(repo => repo.description)
    .sort((a, b) => b.stargazers_count - a.stargazers_count)
)
</script>
