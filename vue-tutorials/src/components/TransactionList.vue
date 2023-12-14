<template>
  <div class="TITLE text-xl font-bold">History</div>
  <div class="BAR h-[0.3px] w-full bg-gray-700"></div>
  <ul class="TRANSACTION-HISTORY flex flex-col gap-2">
    <li
      v-for="transaction in transactions"
      :key="transaction.id"
      class="bg-white relative"
    >
      <!-- delete button -->

      <button
        @click="deleteTransaction(transaction.id)"
        class="bg-red-600 w-[22px] text-white absolute -left-6 opacity-0 hover:opacity-100"
      >
        X
      </button>

      <button class="flex flex-row w-full justify-between">
        <!--  -->
        <span class="LEFT px-2">{{ transaction.text }}</span>
        <!--  -->
        <div class="RIGHT flex flex-row">
          <span class="px-2">{{
            transaction.amount < 0
              ? '-$' + Number(-transaction.amount)
              : '$' + Number(transaction.amount)
          }}</span>
          <div
            :class="transaction.amount < 0 ? 'bg-red-600' : 'bg-green-600'"
            class="STAND-BAR w-[2px] h-[30px]"
          ></div>
        </div>
      </button>
    </li>
    <!-- if transaction is empty -->
    <div
      v-if="transactions.length <= 0"
      class="TRANSACTION-EMPTY text-base font-bold text-center"
    >
      No Transaction...
    </div>
  </ul>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'
// defining props
const props = defineProps({
  transactions: {
    type: Array,
    require: true
  }
})

const emit = defineEmits(['deleteTransaction'])

const deleteTransaction = (id) => {
  emit('deleteTransaction', id)
}

console.log(props.transactions)
</script>
