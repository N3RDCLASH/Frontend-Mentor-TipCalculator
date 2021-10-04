<template>
  <button
    v-if="amount"
    :class="['tip-button', { active: activeTipPercentage === amount }]"
    :onclick="this.setActiveStatus"
  >
    {{ amount }}%
  </button>
  <input v-else type="number"  placeholder="Custom" class="calculator-input" />
</template>

<script>
export default {
  props: {
    amount: Number,
    setActive: Function,
    activeTipPercentage: Number,
  },
  methods: {
    setActiveStatus() {
      return this.setActive(this.amount);
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