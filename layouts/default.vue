<script setup>
// Link to Google Fonts
import AppHeader from "~/components/app-header.vue";

useHead({
  link: [
    {
      rel: 'preconnect',
      href: 'https://fonts.googleapis.com'
    },
    {
      rel: 'stylesheet',
      href: 'https://fonts.googleapis.com/css2?family=Inter&display=swap',
      crossorigin: ''
    }
  ]
})
</script>

<template>
  <div class="container mx-auto max-w-4xl">
    <AppHeader />
    <main class="my-10">
      <slot />
    </main>
  </div>
</template>

<style>
body {
  /* Set the font family for the entire site */
  font-family: 'Inter', sans-serif;
  /* Set the background color for the entire site */
  @apply
  dark:bg-gray-900 bg-white
}
</style>