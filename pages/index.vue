<script setup>
import { transactionViewOptions } from "~/constants";

const selectedView = ref(transactionViewOptions[1])
const isOpen = ref(false)
const { current, previous } = useSelectedTimePeriod(selectedView)
const {
  pending,
  refresh,
  transactions: {
    incomeCount,
    expenseCount,
    incomeTotal,
    expenseTotal,
    grouped: {
      byDate
    }
  }
} = useFetchTransactions(current)
// await refresh() TODO: why

const {
    refresh: refreshPrevious, // TODO: why
    transactions: {
      incomeTotal: previousIncomeTotal,
      expenseTotal: previousExpenseTotal,
    }
} = useFetchTransactions(previous)
// await refreshPrevious() TODO: why
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
    <Trend color="green" title="Income" :amount="incomeTotal" :last-amount="previousIncomeTotal" :loading="pending" />
    <Trend color="red" title="Expense" :amount="expenseTotal" :last-amount="previousExpenseTotal" :loading="pending" />
    <Trend color="green" title="Investments" :amount="4000" :last-amount="5000" :loading="pending" />
    <Trend color="red" title="Saving" :amount="4000" :last-amount="4100" :loading="pending" />
  </section>
  <section class="flex justify-between mb-10">
    <div>
      <h2 class="text-2xl font-extrabold">Transactions</h2>
      <div class="text-gray-500 dark:text-gray-400">
        You have {{ incomeCount }} incomes and {{ expenseCount }} expenses this period
      </div>
    </div>
    <div>
      <TransactionModal v-model="isOpen" @saved="refresh()" />
      <UButton
          icon="i-heroicons-plus-circle"
          color="white"
          variant="solid"
          label="Add"
          @click="isOpen = true" />
    </div>
  </section>
  <section v-if="!pending">
    <div v-for="(transactionsOnDay, date) in byDate" :key="date" class="mb-10">
      <DailyTransactionSummary :date="date" :transactions="transactionsOnDay" />
      <Transaction
          v-for="transaction in transactionsOnDay"
          :key="transaction.id"
          :transaction="transaction"
          @deleted="refresh()" />
    </div>
  </section>
  <section v-else>
    <USkeleton class="h-8 w-full mb-2" v-for="i in 4" :key="i" />
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