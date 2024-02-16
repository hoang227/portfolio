
import type { errorMessages } from 'vue/compiler-sfc';
<template>
  <div>
    projects
  </div>

  <section v-if="pending">loading ...</section>
  <section v-else-if="error">something went wrong ...</section>
  <section v-else>here we display the repos</section>
</template>

<script setup>
const { error, pending, data } = await useFetch('https://api.github.com/users/hoang227/repos')
</script>
