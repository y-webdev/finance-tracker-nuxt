<script setup>
const { currency } = useCurrency(3000)
const items = [
  [
    {
      label: 'Edit',
      icon: 'i-heroicons-pencil-square-20-solid',
      click: () => console.log('Edit')
    },
    {
      label: 'Delete',
      icon: 'i-heroicons-trash-20-solid',
      click: () => console.log('Delete')
    }
  ]
]
</script>

<template>
  <div class="transaction-container">
    <div class="info-container">
      <div class="icon-container">
        <UIcon name="i-heroicons-arrow-up-right" class="text-green-600" />
        <div>Salary</div>
      </div>
      <div>
        <UBadge color="white">Category</UBadge>
      </div>
    </div>
    <div class="amount-container">
      <div>{{ currency }}</div>
      <div>
        <UDropdown :items="items" :popper="{ placement: 'bottom-start' }">
          <UButton color="white" variant="ghost" trailing-icon="i-heroicons-ellipsis-horizontal" />
        </UDropdown>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .transaction-container {
    @apply
    grid grid-cols-2
    py-4
    border-b border-gray-200 dark:border-gray-800
    text-gray-900 dark:text-gray-100
  }

  .info-container {
    @apply
    flex items-center justify-between
  }

  .icon-container {
    @apply
    flex items-center space-x-1
  }

  .amount-container {
    @apply
    flex items-center justify-end space-x-2
  }
</style>