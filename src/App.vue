<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
<!--    <button v-on:click="counter++">Increase</button>-->
<!--    <button @click="counter++">Increase</button>-->
        <button @click="increase(2, $event)">Increase</button>
        <button @click="resetCounter">Reset Counter</button>
    {{ counter }}
    <label for="test">test
      <input
        id="test"
        type="text"
        @blur="blur"
        @focus="focus"
      >
    </label>
    <CalculatorComp/>
  </div>
</template>

<script>
import CalculatorComp from '@/components/CalculatorComp.vue';
import HelloWorld from './components/HelloWorld.vue';

export default {
  name: 'App',
  components: {
    CalculatorComp,
    HelloWorld,
  },
  data: () => ({
    counter: 0,
  }),
  methods: {
    increase(step, event) {
      // eslint-disable-next-line no-plusplus
      this.counter += step;
      console.log(event);
    },
    resetCounter() {
      this.counter = 0;
    },
    blur() {
      console.log('blur');
    },
    focus() {
      console.log('focus');
    },
  },
};
</script>

<style lang="sass">
#app
  font-family: Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50
  margin-top: 60px

</style>
