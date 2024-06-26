<script setup>
  const props = defineProps({
    title: String,
    amount: Number,
    lastAmount: Number,
    color: String,
    loading: Boolean
  })
  const { amount } = toRefs(props)

  const heroIcons = {
    up: 'i-heroicons-arrow-trending-up',
    down: 'i-heroicons-arrow-trending-down'
  }
  const { currency } = useCurrency(amount)
  const trendingUp = computed(
      () => props.amount >= props.lastAmount
  )
  const icon = computed(
      () => trendingUp.value ? heroIcons.up : heroIcons.down
  )
  const percentageTrend = computed(() => {
    if (props.amount === 0 || props.lastAmount === 0) return '∞%'
    const bigger = Math.max(props.amount, props.lastAmount)
    const lower = Math.min(props.amount, props.lastAmount)
    const ratio = ((bigger - lower) / lower) * 100
    return `${Math.ceil(ratio)}%`
  })
</script>

<template>
  <div>
    <div class="title" :class="[color]">{{ title }}</div>

    <div class="amount-container">
      <USkeleton class="h-8 w-full" v-if="loading" />
      <div v-else>{{ currency }}</div>
    </div>

    <div>
      <USkeleton class="h-6 w-full" v-if="loading" />
      <div v-else class="icon-container">
        <UIcon
            :name="icon"
            class="w-6 h-6"
            :class="{'green': trendingUp, 'red': !trendingUp }" />
        <div class="text-gray-500 dark:text-gray-400">
          {{ percentageTrend }} vs last period
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .title {
    @apply
    font-bold
  }

  .green {
    @apply
    text-green-600 dark:text-green-400
  }

  .red {
    @apply
    text-red-600 dark:text-red-400
  }

  .amount-container {
    @apply
    text-2xl font-extrabold text-black dark:text-white
    mb-2
  }

  .icon-container {
    @apply
    flex space-x-1 items-center
    text-sm
  }
</style>