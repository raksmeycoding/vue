<template>
  <div class="font-bold text-xl incomeExpense">
    <h3>YOUR BALANCE</h3>
    <h3>${{ total }}</h3>
  </div>
</template>

<script setup>
import { defineProps } from 'vue'
defineProps({
  total: {
    // eslint-disable-next-line vue/require-prop-type-constructor
    type: Number ,
    require: true
  }
})
</script>
