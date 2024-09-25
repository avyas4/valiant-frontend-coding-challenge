<script setup>
import { ref } from 'vue'
import lang from '../lang/v-form.lang.json'

const props = defineProps({
  /**
   * set the min value for input field
   */
  min: {
    type: Number,
    default: 10,
    Required: false,
  },
  /**
   * set the max value for input field
   */
  max: {
    type: Number,
    default: 100,
    Required: false,
  },
})

const emit = defineEmits(['hasError'])

const modelValue = defineModel('modelValue', { type: String, default: '' })

const isError = ref(false)

/**
 * Functions to allow only numbers
 */
const onlyNumber = (event) => {
  if (!/\d/.test(event.key) && event.key !== '.') return event.preventDefault()
}

/**
 * Emit error for min and max model value change
 */
const validatedInput = () => {
  if (modelValue.value < props.min || modelValue.value > props.max) {
    isError.value = true
  } else {
    isError.value = false
  }
  emit('hasError', isError.value)
}

</script>

<template>
  <div class="sm:col-span-3">
    <label
      for="loan-amount"
      class="vl-required block text-sm font-medium leading-6 text-gray-900"
    >{{ lang.vlLoanAmountLabel }}</label>
    <div class="mt-2">
      <input
        v-model="modelValue"
        type="text"
        :min="min"
        :max="max"
        name="loan-amount"
        autocomplete="given-name"
        class="block w-full rounded-md border-0 px-2 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:max-w-xs sm:text-sm sm:leading-6"
        @keypress="onlyNumber"
        @blur="validatedInput"
      >
      <div
        class="h-6 rounded-lg text-sm text-red-700 dark:text-red-700"
        role="alert"
      >
        <span
          v-if="isError"
          class="text-sm"
        >{{ `This field must be between ${min} and ${max}` }}</span>
      </div>
    </div>
  </div>
</template>

<style>
</style>
