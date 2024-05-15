<script setup>
const props = defineProps({
  date: String,
  transactions: Array,
})
const sum = computed(() => {
  let sum = 0
  for (const transaction of props.transactions) {
    if (transaction.type === 'Income') {
      sum += transaction.amount
    } else {
      sum -= transaction.amount
    }
  }
  return sum
})
const { currency } = useCurrency(sum)
</script>

<template>
  <div class="transaction-container">
    <div class="date-container">
      {{ date }}
    </div>
    <div class="amount-container">
      {{ currency }}
    </div>
  </div>
</template>

<style scoped>
  .transaction-container {
    @apply
    grid grid-cols-2
    py-4
    border-b border-gray-200 dark:border-gray-800
    text-gray-500 dark:text-gray-400
    font-bold
  }

  .date-container {
    @apply
    flex items-center justify-between
  }

  .amount-container {
    @apply
    flex items-center justify-end space-x-2
    mr-10
  }
</style>