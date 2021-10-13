<template>
  <button
    v-if="amount"
    :class="['tip-button', { active: activeTipPercentage === amount }]"
    :onclick="this.setActiveStatus"
  >
    {{ amount }}%
  </button>
  <input
    v-else
    type="number"
    v-model="customAmount"
    :oninput="setActiveStatus"
    placeholder="Custom"
    min="0"
    :class="['calculator-input', { active: activeTipPercentage === amount }]"
  />
</template>

<script>
export default {
  props: {
    amount: Number,
    setActivePercentage: Function,
    activeTipPercentage: Number,
  },
  data() {
    return {
      customAmount: 0,
    };
  },
  methods: {
    setActiveStatus() {
      if (this.customAmount !== 0) {
        return this.setActivePercentage(this.customAmount);
      }
      this.resetInputAmount();
      return this.setActivePercentage(this.amount);
    },
    resetInputAmount() {
      this.customAmount = 0;
    },
  },
  watch: {
    activeTipPercentage(val) {
      if (this.activeTipPercentage !== this.customAmount) this.customAmount = 0;
    },
  },
};
</script>

<style lang="postcss" scoped>
.tip-button {
  @apply max-w-full h-10 text-white rounded;
  background-color: var(--very-dark-cyan);
  font-family: var(--font);
  font-weight: 400;
}
.tip-button:focus,
.tip-button.active {
  background-color: var(--strong-cyan);
}
.tip-button:hover {
  background-color: hsl(173deg 61% 77%);
}
</style>