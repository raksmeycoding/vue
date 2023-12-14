<template>
  <h3 class="text-2xl font-bold">Add new transaction</h3>
  <div class="BAR h-[0.3px] w-full bg-gray-700"></div>
  <form
    @submit.prevent="onSubmit"
    class="flex flex-col gap-4"
  >
    <div class="flex flex-col gap-2">
      <label
        class="font-bold text-sm"
        for="text"
        >Text</label
      >
      <input
        class="outline-none px-1 py-1"
        type="text"
        id="text"
        v-model="text"
        placeholder="Enter text..."
      />
    </div>
    <div class="flex flex-col gap-2">
      <label
        class="font-bold text-sm"
        for="amount"
        >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input
        class="outline-none px-1 py-1"
        type="text"
        id="amount"
        v-model="amount"
        placeholder="Enter amount..."
      />
    </div>
    <button
      type="submit"
      class="font-bold text-md bg-purple-600 text-white px-1 py-1"
    >
      Add transaction
    </button>
  </form>
</template>

<script setup>
import { ref, defineEmits } from 'vue'
import { useToast } from 'vue-toastification'
const text = ref('')
const amount = ref('')
const emit = defineEmits(['transactionSubmitted'])
const toast = useToast()

const onSubmit = () => {
  if (text.value == '' || amount.value === '') {
    toast.error('Both fields must be filled')
    throw new Error('Value must be exist.')
  }

  if (!Number(amount.value)) {
    toast.error('Amount must be a number')
    throw new Error('Amount must be a number')
  }

  const transactionDate = {
    text: text.value,
    amount: parseInt(amount.value)
  }
  emit('transactionSubmitted', transactionDate)
}
</script>
