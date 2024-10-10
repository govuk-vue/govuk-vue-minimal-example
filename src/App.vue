<script setup lang="ts">
import { ref, computed } from 'vue'

const itemPrice = ref(null)
const vatRate = 0.2

const priceWithVat = computed(() => {
  const parsedItemPrice = parseFloat(itemPrice.value);

  if(!isNaN(parsedItemPrice)) {
    const formatter = new Intl.NumberFormat('en-GB', { style: 'currency', currency: 'GBP' })
    return formatter.format(parsedItemPrice * (1 + vatRate))
  }
})

function continueClicked() {
  alert('You clicked the continue button')
}
</script>

<template>
  <gv-header/>
  <div class="govuk-width-container">
    <main class="govuk-main-wrapper">
      <div class="govuk-grid-row">
        <div class="govuk-grid-column-two-thirds">
          <h1 class="govuk-heading-xl">Welcome to GOV.UK Vue</h1>
          <p class="govuk-body-l">
            This is a minimal example of how to set up <a href="https://govukvue.org" class="govuk-link">GOV.UK Vue</a> in a new project. This is not a real government service.
          </p>

          <p class="govuk-body">
            The rest of this page contains examples of GOV.UK Vue components.
          </p>

          <gv-input v-model="itemPrice" prefix="£" suffix="per item" :spellcheck="false" classes="govuk-input--width-4">
            <template #label>
              What is the cost per item excluding VAT, in pounds?
            </template>
          </gv-input>
          <gv-inset-text v-if="priceWithVat" aria-live="polite">
            The total cost per item, including VAT, is {{ priceWithVat }}
          </gv-inset-text>

          <gv-button @click="continueClicked">Continue</gv-button>
        </div>
      </div>
    </main>
  </div>
  <gv-footer/>
</template>
