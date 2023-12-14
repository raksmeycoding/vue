<template>
  <div class="incomeExpense flex flex-row justify-between items-center gap-8 px-8 bg-white">
    <!--  -->
    <div class="INCOME">
      <div class="incomeText">INCOME</div>
      <div class="PRICE text-green-600">${{ income }}</div>
    </div>
    <!--  -->
    <div class="EXPENSE">
      <div class="incomeText">EXPENSE</div>
      <div class="PRICE text-red-600">-${{ expense }}</div>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue'

defineProps({
  income: {
    type: Number,
    require: true
  },
  expense: {
    type: Number,
    require: true
  }
})
</script>
