<script setup>
const props = defineProps({
  transaction: Object,
})
const emit = defineEmits(['deleted'])
const { currency } = useCurrency(props.transaction.amount)
const isLoading = ref(false)
const toast = useToast()
const supabase = useSupabaseClient()
const transactionOptions = {
  income: ['i-heroicons-arrow-up-right', 'text-green-600'],
  expense: ['i-heroicons-arrow-down-left', 'text-red-600']
}
const transactionIcon = computed(
    () => transactionOptions[props.transaction.type.toLowerCase()][0]
)

const transactionColor = computed(
    () => transactionOptions[props.transaction.type.toLowerCase()][1]
)

const deleteTransaction = async () => {
  isLoading.value = true

  try {
    await supabase.from('transactions')
        .delete()
        .eq('id', props.transaction.id)
    toast.add({
      title: 'Transaction deleted successfully.',
      icon: 'i-heroicons-check-circle',
      color: 'green'
    })
    emit('deleted', props.transaction.id)
  } catch (error) {
    toast.add({
      title: 'Transaction not deleted.',
      icon: 'i-heroicons-exclamation-circle',
      color: 'red'
    })
  } finally {
    isLoading.value = false
  }
}
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
      click: deleteTransaction
    }
  ]
]
</script>

<template>
  <div class="transaction-container">
    <div class="info-container">
      <div class="icon-container">
        <UIcon :name="transactionIcon" :class="[transactionColor]" />
        <div>{{ transaction.description }}</div>
      </div>
      <div>
        <UBadge color="white" v-if="transaction.category">{{ transaction.category }}</UBadge>
      </div>
    </div>
    <div class="amount-container">
      <div>{{ currency }}</div>
      <div>
        <UDropdown :items="items" :popper="{ placement: 'bottom-start' }">
          <UButton color="white" variant="ghost" trailing-icon="i-heroicons-ellipsis-horizontal" :loading="isLoading" />
        </UDropdown>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .transaction-container {
    @apply
    grid grid-cols-3
    py-4
    border-b border-gray-200 dark:border-gray-800
    text-gray-900 dark:text-gray-100
  }

  .info-container {
    @apply
    flex items-center justify-between col-span-2
    space-x-4
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