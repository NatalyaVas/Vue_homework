<template>
  <div>
    <div class="main">
      <input id="op1" type="number" v-model.number="op1">
      <input id="op2" type="number" v-model.number="op2">
      = {{ result }} <br/>
      Fibonacci-1 =  {{ fib1 }}<br/>
      Fibonacci-2 =  {{ fib2() }}<br/>
    </div>
<!--    <div class="error" v-if="error">-->
<!--      Ошибка: {{ error }}-->
<!--    </div>-->
    <div class="error" v-show="error">
      Ошибка: {{ error }}
    </div>
    <div class="messages">
      <template v-if="result < 0">Отрицательный результат</template>
      <template v-else-if="result < 100">Результат в первой сотне</template>
      <template v-else>Простое условие</template>
    </div>
    <div class="keyboard">
<!--      <button @click="result = op1 + op2">+</button>-->
<!--      <button @click="calculate('+')">+</button>-->
<!--      <button @click="calculate('-')">-</button>-->
<!--      <button @click="calculate('/')">/</button>-->
<!--      <button @click="calculate('*')">*</button>-->
<!--      <div v-for="(item, index) in collection" :key="item">-->
<!--        {{ index }} - {{ item }}-->
<!--      </div>-->
      <button
        v-for="operator in operators"
        @click="calculate(operator)"
        :title="operator"
        :key="operator"
      >
        {{ operator }}
      </button>
    </div>
    <div class="logs">
      {{ logs }}
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
    error: '',
    operators: ['+', '-', '/', '*', '^', '%'],
    collection: ['1', '2', '3', '4'],
    logs: {},
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
      this.error = '';
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

      // this.logs[Date.now()] = `${op1} ${operation} ${op2}`;
      // не при каждом нажатии срабатывала кнопка
      // this.logs = { ...this.logs, [Date.now()]: `${this.op1} ${operation} ${this.op2}` };
      // Vue set();
      this.$set(this.logs, Date.now(), `${this.op1} ${operation} ${this.op2}`);
    },

    fib(n) {
      return n <= 1 ? n : this.fib(n - 1) + this.fib(n - 2);
    },

    fib2() {
      console.log('metod');
      const { op2 } = this;
      return this.fib(op2);
    },
  },

  computed: {
    fib1() {
      console.log('computed');
      const { op1 } = this;
      return this.fib(op1);
    },
  },
};
</script>

<style scoped>

</style>
