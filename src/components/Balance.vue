<script setup>
import { defineProps } from 'vue'

const props = defineProps({
  total: {
    type: Number,
    required: true
  }
})
</script>

<template>
  <div>
    <h4>Your Balance</h4>
    <h1 id="balance">€{{ total }}</h1>
  </div>
</template>

<style scoped>
div {
  margin-left: -10px;
}
</style>
