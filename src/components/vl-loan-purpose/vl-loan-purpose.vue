<script setup>
import { ref, onMounted } from 'vue'
import fetchAPI from '../../utils/API.js'
import lang from '../lang/v-form.lang.json'

defineEmits(['change'])

const modelValue = defineModel('modelValue', { type: Number, default: 0 })

/* Start section for Loan Purpose */
const getData = ref(null)

async function fetchData () {
  try {
    getData.value = await fetchAPI('/loan-purposes')
  } catch (err) {
    if (err instanceof Error) {
      // Perform your error handling here
    }
  }
}

/* on mount life cycle hook */
onMounted(() => {
  fetchData()
})

/* End */

</script>

<template>
  <div class="sm:col-span-3">
    <label
      for="loan-purpose"
      class="vl-required block text-sm font-medium leading-6 text-gray-900"
    >{{ lang.vlLoanPurposeLabel }}</label>
    <div class="mt-2">
      <select
        v-model="modelValue"
        name="loan-purpose"
        autocomplete="loan-purpose"
        class="block w-full rounded-md border-0 px-2 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:max-w-xs sm:text-sm sm:leading-6"
        @change="$emit('change')"
      >
        <option
          v-for="(item, i) in getData"
          :key="i"
          :value="item.annualRate"
        >
          {{ item.label }}<option />
        </option>
      </select>
    </div>
  </div>
</template>

<style>
</style>
