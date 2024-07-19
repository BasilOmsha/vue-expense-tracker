<!-- Options api -->
<!-- <script>
import Header from '../components/Header.vue'
import Balance from '../components/Balance.vue'
import IncomeExpenses from '@/components/IncomeExpenses.vue'
import TransactioList from '@/components/TransactioList.vue'
import AddTransaction from '@/components/AddTransaction.vue'

// in the traditional way components need to be registred to show up
export default {
  components: {
    Header,
    Balance,
    IncomeExpenses,
    TransactioList,
    AddTransaction
  }
}
</script> -->

<!-- new composition api -->
<script setup>
import Header from '../components/Header.vue'
import Balance from '../components/Balance.vue'
import IncomeExpenses from '@/components/IncomeExpenses.vue'
import TransactioList from '@/components/TransactioList.vue'
import AddTransaction from '@/components/AddTransaction.vue'
import { useToast } from 'vue-toastification'

import { ref, computed, onMounted } from 'vue'

const toast = useToast()

const transactions = ref([
  // { id: 1, text: 'Flower', amount: -19.99 },
  // { id: 2, text: 'Salary', amount: 299.97 },
  // { id: 3, text: 'Book', amount: -10 },
  // { id: 4, text: 'Camera', amount: 150 }
])

// similar to useEffect in React
onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'))

  if (savedTransactions) {
    transactions.value = savedTransactions
  }
})

// console.log(transactions.value)

// Get Total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0)
})

// Get Income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
    .toFixed(2) // toFixed adds decimals
})

// Get Expenses
const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
    .toFixed(2) // toFixed adds decimals
})

// Add transaction
const handleTransactionSubmitted = (transactionData) => {
  // console.log(transactionData)
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount
  })
  // console.log(generateUniqueId())

  saveTransactionsToLocalStorage()

  toast.success('Transaction Added!')
}

// Generate unique ID
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000)
}

// Delete a transaction
const handleTransactionDeleted = (id) => {
  // console.log(id)
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id)

  saveTransactionsToLocalStorage()

  toast.success('Transaction Deleted!')
}

// Save to local storage (when adding and deleting)
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}
</script>

<template>
  <main>
    <!-- <div class="mainPage"> -->
    <Header />
    <div class="container">
      <!-- v-bind can be removed -->
      <Balance v-bind:total="+total" />
      <!-- + sign to pass props as numbers-->
      <IncomeExpenses :income="+income" :expenses="+expenses" />
      <!-- passing transactions as a prop to the component -->
      <TransactioList :transactions="transactions" @transactionDeleted="handleTransactionDeleted" />
      <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
    </div>
    <!-- </div> -->
  </main>
</template>
