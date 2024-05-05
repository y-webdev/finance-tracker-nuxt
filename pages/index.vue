<script setup>
import { transactionViewOptions } from "~/composable/constants.js";

const selectedView = ref(transactionViewOptions[1])
</script>

<template>
  <section>
    <h1>
      Summary
    </h1>
    <div>
      <USelectMenu v-model="selectedView" :options="transactionViewOptions" />
    </div>
  </section>
</template>

<style scoped>
  section {
    @apply
    flex items-center justify-between
    mb-10
  }

  h1 {
    @apply
    text-4xl font-extrabold
  }
</style>