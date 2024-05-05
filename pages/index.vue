<script setup>
import { transactionViewOptions } from "~/constants";

const selectedView = ref(transactionViewOptions[1])
</script>

<template>
  <section class="summary">
    <h1>
      Summary
    </h1>
    <div>
      <USelectMenu v-model="selectedView" :options="transactionViewOptions" />
    </div>
  </section>
  <section class="trend">
    <Trend color="green" title="Income" :amount="4000" :last-amount="3000" :loading="false" />
    <Trend color="red" title="Expense" :amount="4000" :last-amount="3000" :loading="false" />
    <Trend color="green" title="Investments" :amount="4000" :last-amount="5000" :loading="false" />
    <Trend color="red" title="Saving" :amount="4000" :last-amount="4100" :loading="false" />
  </section>
</template>

<style scoped>
  .summary {
    @apply
    flex items-center justify-between
    mb-10
  }

  .summary h1 {
    @apply
    text-4xl font-extrabold
  }

  .trend {
    @apply grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 sm:gap-16 mb-10
  }
</style>