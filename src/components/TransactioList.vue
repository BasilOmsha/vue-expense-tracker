<!-- <script>
// Options API way
// export default {
//   data() {
//     return {
//       transactions: [
//         { id: 1, text: 'Flower', amount: -19.99 },
//         { id: 2, text: 'Salary', amount: 299.97 },
//         { id: 3, text: 'Book', amount: -10 },
//         { id: 4, text: 'Camera', amount: 150 }
//       ]
//     }
//   }
// }

// Composition api
export default {
  setup() {
    const transactions = [
      { id: 1, text: 'Flower', amount: -19.99 },
      { id: 2, text: 'Salary', amount: 299.97 },
      { id: 3, text: 'Book', amount: -10 },
      { id: 4, text: 'Camera', amount: 150 }
    ]
    return {
      transactions
    }
  }
}
</script> -->

<!-- Newer composition api -->
<script setup>
// const transactions = [
//   { id: 1, text: 'Flower', amount: -19.99 },
//   { id: 2, text: 'Salary', amount: 299.97 },
//   { id: 3, text: 'Book', amount: -10 },
//   { id: 4, text: 'Camera', amount: 150 }
// ]
import { defineProps } from 'vue'

const emit = defineEmits(['transactionDeleted'])

const props = defineProps({
  transactions: {
    type: Array,
    required: true
  }
})

const deleteTransaction = (id) => {
  emit('transactionDeleted', id)
}
</script>

<template>
  <h3>Transactions</h3>
  <ul id="list" class="list">
    <ul id="list" class="list">
      <!-- For looping we are using the v-for directive -->
      <!-- <li
        v-for="transaction in transactions"
        v-bind:key="transaction.id"
        v-bind:class="transaction.amount < 0 ? 'minus' : 'plus'"
      >
        {{ transaction.text }} <span>{{ transaction.amount }}</span
        ><button class="delete-btn">x</button>
      </li> -->
      <!-- or: -->
      <li
        v-for="transaction in transactions"
        :key="transaction.id"
        :class="transaction.amount < 0 ? 'minus' : 'plus'"
      >
        {{ transaction.text }} <span>${{ transaction.amount }}</span
        ><button @click="deleteTransaction(transaction.id)" class="delete-btn">x</button>
      </li>
    </ul>
    <!-- <li class="minus">Cash <span>-$400</span><button class="delete-btn">x</button></li>
    <li class="plus">Paycheck <span>$780</span><button class="delete-btn">x</button></li> -->
  </ul>
</template>
