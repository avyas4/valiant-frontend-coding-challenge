<script setup>

defineProps({
  /**
   * Validation object of errors
   */
  errors: {
    type: Object,
    default: () => {},
    Required: false,
  },
  /**
   * Validation flag for requested loan amount
   */
  isLoanAmountValid: {
    type: Boolean,
    Required: false,
  },
  /**
   * Validation flag for repayment period
   */
  isRepaymentPeriodsValid: {
    type: Boolean,
    Required: false,
  },
  /**
   * Validation flag for loan term
   */
  isLoanTermValid: {
    type: Boolean,
    Required: false,
  },
  /**
   * Validation flag for loan purpose
   */
  isLoanPurposeValid: {
    type: Boolean,
    Required: false,
  },
})

</script>

<template>
  <ul class="mt-1.5 list-inside list-disc">
    <li
      v-if="errors?.isLoanAmountValid && !isLoanAmountValid"
      class="text-sm text-red-700"
    >
      {{ errors.isLoanAmountValid }}
    </li>
    <li
      v-if="errors?.isLoanPurposeValid && !isLoanPurposeValid"
      class="text-sm text-red-700"
    >
      {{ errors.isLoanPurposeValid }}
    </li>
    <li
      v-if="errors?.isRepaymentPeriodsValid && !isRepaymentPeriodsValid"
      class="text-sm text-red-700"
    >
      {{ errors.isRepaymentPeriodsValid }}
    </li>
    <li
      v-if="errors?.isLoanTermValid && !isLoanTermValid"
      class="text-sm text-red-700"
    >
      {{ errors.isLoanTermValid }}
    </li>
  </ul>
</template>

<style>
</style>
