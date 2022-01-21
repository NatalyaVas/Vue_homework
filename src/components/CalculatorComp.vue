<template>
  <div>
    <div class="main">
      <input id="op1" type="number" v-model.number="op1">
      <input id="op2" type="number" v-model.number="op2">
      = {{ result }} <br/>
    </div>
    <div class="keyboard">
      <button
        v-for="operator in operators"
        @click="calculate(operator)"
        :title="operator"
        :key="operator"
      >
        {{ operator }}
      </button>
    </div>
    <div>
      <input type="checkbox" id="keyboard" v-model="checkedKeyboard" :checked="checkedKeyboard">
      <label for="keyboard">Показать клавиатуру</label>
    </div>
    <div v-show="checkedKeyboard">
      <div>
        <input id="operand1" type="radio" value="op1" v-model="checkedOperand">
        <label for="operand1">Операнд 1</label>
        <input id="operand2" type="radio" value="op2" v-model="checkedOperand">
        <label for="operand2">Операнд 2</label>
      </div>
      <div>
        <button
          v-for="item of items"
          :key="item"
          @click="keyboardClick(item)"
        >
         {{ item }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CalculatorComp',
  data: () => ({
    op1: 0,
    op2: 0,
    result: 0,
    operators: ['+', '-', '/', '*', '^', '%'],
    items: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
    checkedKeyboard: false,
    checkedOperand: 'op1',
  }),
  methods: {
    sum() {
      this.result = this.op1 + this.op2;
    },

    sub() {
      this.result = this.op1 - this.op2;
    },

    div() {
      const { op1, op2 } = this;

      if (op2 === 0) this.error = 'На ноль делить нельзя.';
      else this.result = op1 / op2;
    },

    mult() {
      this.result = this.op1 * this.op2;
    },

    pow() {
      this.result = this.op1 ** this.op2;
    },

    trunc() {
      this.result = Math.trunc(this.op1 / this.op2);
    },

    calculate(operation) {
      // eslint-disable-next-line default-case
      switch (operation) {
        case '+':
          this.sum();
          break;
        case '-':
          this.sub();
          break;
        case '/':
          this.div();
          break;
        case '*':
          this.mult();
          break;
        case '^':
          this.pow();
          break;
        case '%':
          this.trunc();
          break;
      }
    },
    keyboardClick(item) {
      if (typeof this[this.checkedOperand] === 'number') {
        this[this.checkedOperand] = Number(`${this[this.checkedOperand]} ${item}`);
      }
    },
    backSpace() {
      if (typeof this[this.checkedOperand] === 'number') {
        this[this.checkedOperand] = Math.trunc(this[this.checkedOperand] / 10);
      }
    },
  },
};
</script>

<style scoped>

</style>
