<template>
  <v-container>
    <v-col cols="12" sm="6">
      <v-text-field label="Left Value" single-line v-model.number="leftValue" />
    </v-col>

    <v-col class="d-flex" cols="12" sm="6">
      <v-select
        label="Calc Type"
        :items="types"
        v-model.number="calcType"
      ></v-select>
    </v-col>

    <v-col cols="12" sm="6">
      <v-text-field
        label="Right Value"
        single-line
        v-model.number="rightValue"
      />
    </v-col>

    <v-col cols="12" sm="6">
      =
    </v-col>

    <v-col cols="12" sm="6">
      <v-text-field label="Result" single-line v-model.number="resultValue" />
    </v-col>
  </v-container>
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
      types: [
        { text: "+", value: CalcType.Addition },
        { text: "-", value: CalcType.Subtraction },
        { text: "*", value: CalcType.Multiplication },
        { text: "/", value: CalcType.Division }
      ],
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
