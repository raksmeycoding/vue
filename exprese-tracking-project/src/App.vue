<template>
  <div class="main container mx-auto max-sm:px-2 flex items-center justify-center h-screen">
    <div class="WRAPPER flex flex-col w-[500px] gap-4">
      <Header />
      <Balance :total="+total" />
      <IncomeExpense
        :income="+income"
        v-bind:expense="-expense"
      />
      <TransactionList
        @deleteTransaction="deleteTransactionHandler"
        :transactions="transactions"
      />
      <AddTransaction @transactionSubmitted="handleTransactionSubmittedEvent" />
    </div>
  </div>
</template>

<script setup>
import Header from './components/Header.vue'
import Balance from './components/Balance.vue'
import IncomeExpense from './components/IncomeExpense.vue'
import TransactionList from './components/TransactionList.vue'
import AddTransaction from './components/AddTransaction.vue'
import { useToast } from 'vue-toastification'
import { ref, computed, watch, onMounted } from 'vue'

onMounted(() => {
  const transactionList = JSON.parse(localStorage.getItem('transactions'))
  transactionList ? (transactions.value = transactionList) : null
})

const transactions = ref([
  { id: 1, text: 'Flower', amount: -99.99 },
  { id: 2, text: 'Salary', amount: 810.99 },
  { id: 3, text: 'Book', amount: -9.99 },
  { id: 4, text: 'Camera', amount: -300.999 }
])

const toast = useToast()
const total = computed(() => {
  return transactions.value
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
    .toFixed(2)
})

// eslint-disable-next-line no-unused-vars
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, income) => {
      return acc + income.amount
    }, 0)
    .toFixed(2)
})

const expense = computed(() => {
  return transactions.value
    .filter((transaction) => {
      return transaction.amount < 0
    })
    .reduce((acc, current) => {
      return acc + current.amount
    }, 0)
    .toFixed(2)
})

const handleTransactionSubmittedEvent = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    ...transactionData
  })

  saveTransactionsToLocalStorage()

  toast.success('Transaction added')
}

const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000)
}

watch(
  () => transactions.value.length,
  (newValue, oldValue) => {
    console.log('Transactions ', transactions.value)
  }
)

const deleteTransactionHandler = (id) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id)
  toast.success('Transaction deleted')
  saveTransactionsToLocalStorage()
}

const saveTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}
</script>
