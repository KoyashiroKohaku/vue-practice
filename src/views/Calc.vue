<template>
  <v-container>
    <v-form v-model="isValid">
      <v-col cols="12" sm="6">
        <v-text-field
          label="Left Value"
          single-line
          v-model.number="leftValue"
          :rules="inputRules"
        />
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
          :rules="inputRules"
        />
      </v-col>

      <v-col cols="12" sm="6">
        =
      </v-col>

      <v-col cols="12" sm="6">
        <v-text-field label="Result" single-line v-model.number="resultValue" />
      </v-col>
    </v-form>
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
      isValid: false,
      types: [
        { text: "+", value: CalcType.Addition },
        { text: "-", value: CalcType.Subtraction },
        { text: "*", value: CalcType.Multiplication },
        { text: "/", value: CalcType.Division }
      ],
      leftValue: "",
      rightValue: "",
      calcType: CalcType.Addition,
      inputRules: [
        (v: string) => v.length !== 0 || "Value is required",
        (v: string) => Number.isFinite(Number(v)) || "Value is not a number"
      ]
    };
  },
  computed: {
    resultValue(): number | null {
      if (!this.isValid) {
        return null;
      }

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
          return null;
      }
    }
  }
});
</script>
