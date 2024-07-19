<script>
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
</script>

<!-- <script setup>
import Header from '../components/Header.vue'
import Balance from '../components/Balance.vue'
import IncomeExpenses from '@/components/IncomeExpenses.vue'
import TransactioList from '@/components/TransactioList.vue'
import AddTransaction from '@/components/AddTransaction.vue'
</script> -->

<template>
  <main>
    <!-- <div class="mainPage"> -->
    <Header />
    <div class="container">
      <Balance />
      <IncomeExpenses />
      <TransactioList />
      <AddTransaction />
    </div>
    <!-- </div> -->
  </main>
</template>
