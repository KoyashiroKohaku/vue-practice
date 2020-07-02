<template>
  <div class="calc">
    <input type="text" id="left" v-model.number="leftValue" />
    <select v-model.number="calcType">
      <option value="0" selected>+</option>
      <option value="1">-</option>
      <option value="2">*</option>
      <option value="3">/</option>
    </select>
    <input type="text" id="right" v-model.number="rightValue" />
    <span>=</span>
    <input type="text" id="result" v-model.number="resultValue" readonly />
  </div>
</template>

<script lang="ts">
enum CalcType {
  Addition,
  Subtraction,
  Multiplication,
  Division
}

import Vue from "vue";

export default Vue.extend({
  name: "Calc",
  data() {
    return {
      leftValue: 0,
      rightValue: 0,
      calcType: CalcType.Addition
    };
  },
  computed: {
    resultValue(): number {
      switch (this.calcType) {
        case CalcType.Addition:
          return this.leftValue + this.rightValue;
        case CalcType.Subtraction:
          return this.leftValue - this.rightValue;
        case CalcType.Multiplication:
          return this.leftValue * this.rightValue;
        case CalcType.Division:
          return this.leftValue / this.rightValue;
        default:
          return 0;
      }
    }
  }
});
</script>
