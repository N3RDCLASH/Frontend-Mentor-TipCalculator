<template>
  <span class="calc-logo">SPLI</span>
  <br />
  <span class="calc-logo">TTER</span>
  <div class="calculator-container">
    <!--     -->
    <div class="calculator-column-left">
      <div class="calculator-input-container">
        <span class="label">Bill</span>
        <input
          class="calculator-input"
          id="bill"
          type="number"
          placeholder="0"
          v-model="bill"
        />
      </div>
      <span class="label">Select Tip %</span>
      <div class="tip-buttons-container">
        <TipButton
          :setActivePercentage="setActiveTipPercentage"
          :amount="5"
          :activeTipPercentage="activeTipPercentage"
        />
        <TipButton
          :setActivePercentage="setActiveTipPercentage"
          :amount="10"
          :activeTipPercentage="activeTipPercentage"
        />
        <TipButton
          :setActivePercentage="setActiveTipPercentage"
          :amount="15"
          :activeTipPercentage="activeTipPercentage"
        />
        <TipButton
          :setActivePercentage="setActiveTipPercentage"
          :amount="25"
          :activeTipPercentage="activeTipPercentage"
        />
        <TipButton
          :setActivePercentage="setActiveTipPercentage"
          :amount="50"
          :activeTipPercentage="activeTipPercentage"
        />
        <!-- When the amount prop is ommitted from component the button turns into a custom input -->
        <TipButton
          :setActivePercentage="setActiveTipPercentage"
          :activeTipPercentage="activeTipPercentage"
        />
      </div>
      <div class="calculator-input-container">
        <div class="flex justify-between">
          <span class="label">Number of People</span>
          <span v-if="this.numberOfPeople === 0" class="label error"
            >Can't be zero
          </span>
        </div>
        <input
          :class="['calculator-input', { error: this.numberOfPeople === 0 }]"
          placeholder="0"
          id="people"
          type="number"
          v-model="numberOfPeople"
        />
      </div>
    </div>
    <!-- s -->
    <div class="calculator-column-right">
      <div class="tip-amount-container">
        <span class="tip-amount-label">Tip Amount </span>
        <span class="tip-amount">${{ tipAmountPerPerson }} </span>
      </div>
      <div class="total-amount-container">
        <span class="total-amount-label">Total</span>
        <span class="total-amount">${{ totalAmountPerPerson }}</span>
      </div>
      <input
        :onclick="resetValues"
        type="button"
        class="reset-button"
        :disabled="tipAmountPerPerson === 0 && totalAmountPerPerson === 0"
        value="RESET"
      />
    </div>
  </div>
</template>

<script>
import TipButton from "../TipButton/TipButton.vue";
export default {
  components: { TipButton },
  setup() {
    return {};
  },
  data() {
    return {
      bill: 0,
      activeTipPercentage: 0,
      numberOfPeople: 0,
      totalAmount: 0,
    };
  },
  methods: {
    setActiveTipPercentage(tip) {
      console.log(tip);
      return (this.activeTipPercentage = tip);
    },
    resetValues() {
      this.bill = 0;
      this.activeTipPercentage = 0;
      this.numberOfPeople = 0;
      this.totalAmount = 0;
      console.log("Reset");
    },
  },
  computed: {
    tipAmountPerPerson() {
      const calculation =
        (this.bill * this.activeTipPercentage) / 100 / this.numberOfPeople;
      return isNaN(calculation) || calculation === Infinity
        ? Number(0).toFixed(2)
        : calculation.toFixed(2);
    },
    totalAmountPerPerson() {
      const calculation =
        this.bill / this.numberOfPeople + Number(this.tipAmountPerPerson);

      return isNaN(calculation) || calculation === Infinity
        ? Number(0).toFixed(2)
        : calculation.toFixed(2);
    },
  },
};
</script>

<style lang="postcss" scoped>
.calc-logo {
  @apply primary-font very-dark-cyan-text font-bold text-lg;
  letter-spacing: 8px;
}
.calculator-container {
  @apply flex bg-white w-8/12 h-auto mx-auto rounded-lg p-8;
  margin-top: 10vh;
}

/* flex: 2 columns */
.calculator-column-left {
  @apply flex flex-col w-full pr-4;
  margin-right: 1rem;
}
.calculator-column-right {
  @apply flex flex-col w-full px-4 rounded-md bg-very-dark-cyan;
}

/* Tip Amount */
.tip-amount-container,
.total-amount-container {
  @apply flex px-5 py-1 mt-5 text-left justify-between items-center;
}
.tip-amount-label,
.total-amount-label {
  @apply text-white primary-font flex flex-col;
}
.tip-amount-label::after,
.total-amount-label::after {
  @apply text-white primary-font dark-grayish-cyan-2-text;
  content: " / person Total";
  font-size: 10px;
}
.tip-amount,
.total-amount {
  @apply text-white primary-font strong-cyan-text font-bold;
  font-size: 3vw;
}

.reset-button {
  @apply w-full mt-28 p-2 very-dark-cyan-text bg-strong-cyan primary-font mx-auto font-bold rounded;
}

.reset-button:disabled {
  background-color: hsl(183deg 79% 24%);
}
.reset-button:hover:enabled {
  background-color: hsl(173deg 61% 77%);
}

/* Input Styles */
.calculator-input-container {
  @apply w-full py-5 flex-col flex;
}
.calculator-input {
  @apply h-7  rounded p-5 text-right primary-font very-dark-cyan-text font-semibold;
  background-color: var(--light-grayish-cyan-2);
  font-size: var(--form-font-size);
}
.calculator-input:focus-visible {
  @apply outline-none;
}

.calculator-input.error,
.calculator-input.error:focus-visible,
.calculator-input.error:hover:enabled {
  outline: 2px solid hsl(13deg 33% 60%);
}
.calculator-input:focus-visible,
.calculator-input:hover:enabled {
  /* outline-color: hsl(173deg 31% 50%); */
  outline: 2px solid hsl(173deg 31% 50%);
}

.label {
  @apply text-left text-sm my-2 primary-font font-bold dark-grayish-cyan-1-text;
  font-family: var(--font);
}
.label.error {
  color: hsl(13deg 33% 60%);
}

#bill {
  background-image: url("images/icon-dollar.svg");
  background-position: left;
  background-position-x: 1rem;
  background-repeat: no-repeat;
}

#people {
  background-image: url("images/icon-person.svg");
  background-position: left;
  background-position-x: 1rem;
  background-repeat: no-repeat;
}

/* Buttons Container */
.tip-buttons-container {
  @apply grid grid-cols-3 grid-rows-2 gap-2;
}

/* Utility Classes */
.primary-font {
  font-family: var(--font);
}
.strong-cyan-text {
  color: var(--strong-cyan);
}
.very-dark-cyan-text {
  color: var(--very-dark-cyan);
}
.dark-grayish-cyan-1-text {
  color: var(--dark-grayish-cyan-1);
}
.dark-grayish-cyan-2-text {
  color: var(--dark-grayish-cyan-2);
}
.bg-very-dark-cyan {
  background-color: var(--very-dark-cyan);
}
.bg-strong-cyan {
  background-color: var(--strong-cyan);
}
.bg-dark-grayish-cyan-1 {
  background-color: var(--dark-grayish-cyan-1);
}
.bg-dark-grayish-cyan-2 {
  background-color: var(--dark-grayish-cyan-2);
}

/* Custom styling*/
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
/* Firefox */
input[type="number"] {
  -moz-appearance: textfield;
}

@media only screen and (max-width: 982px) {
  .calculator-container {
    @apply flex-col mx-0 w-full;
  }
  .calculator-input-container {
    @apply px-0;
  }
  .reset-button {
    @apply my-10;
  }
  .calculator-input {
    font-size: 24px;
  }
  .calculator-column-left {
    @apply px-0;
  }
}
</style>