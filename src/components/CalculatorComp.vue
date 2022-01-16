<template>
  <div>
    <div class="main">
      <input id="op1" type="number" v-model.number="op1">
      <input id="op2" type="number" v-model.number="op2">
      = {{ result }}
    </div>
    <div class="keyboard">
      <button @click="result = op1 + op2">+</button>
      <button @click="sub">-</button>
      <button @click="div">/</button>
      <button @click="mult">*</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CalculatorComp',
  data: () => ({
    op1: '0',
    op2: '0',
    result: 0,
  }),
  methods: {
    sub() {
      this.result = this.op1 - this.op2;
    },

    div() {
      this.result = this.op1 / this.op2;
    },

    mult() {
      this.result = this.op1 * this.op2;
    },
  },
};
</script>

<style scoped>

</style>
