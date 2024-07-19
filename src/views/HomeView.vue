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

import { ref, computed } from 'vue'

const transactions = ref([
  { id: 1, text: 'Flower', amount: -19.99 },
  { id: 2, text: 'Salary', amount: 299.97 },
  { id: 3, text: 'Book', amount: -10 },
  { id: 4, text: 'Camera', amount: 150 }
])

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
</script>

<template>
  <main>
    <!-- <div class="mainPage"> -->
    <Header />
    <div class="container">
      <!-- v-bind can be removed -->
      <Balance v-bind:total="total" />
      <!-- + sign to pass props as numbers-->
      <IncomeExpenses :income="+income" :expenses="+expenses" />
      <!-- passing transactions as a prop to the component -->
      <TransactioList :transactions="transactions" />
      <AddTransaction />
    </div>
    <!-- </div> -->
  </main>
</template>
