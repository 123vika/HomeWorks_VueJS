<template>
  <div class="calc">
    {{ message }}

    <div>
      <input type="number" placeholder="Operand 1" @focus="onFocus" v-model.number="operand1" key="operand1"/>
      <br>
      <input type="number" placeholder="Operand 2" v-on:keyup="onKeyUp" v-model.number="operand2" key="operand2"/>
      <br>
      = {{ result }}
      <div class="keyboard">
        <button @click="result= operand1 + operand2">+</button>
        <button @click="subtract">-</button>
        <button v-on:click="multi(operand1, operand2)">*</button>
        <button @click="divide(operand1, operand2)">/</button>
        <button v-on:click="pow(operand1, operand2)">*n</button>
      </div>
      <br>
      <button @click="doThan('hello', $event)">Click</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data: () => ({
    message: "Hello Vue!",
    operand1: 0,
    operand2: 0,
    result: 0,
  }),
  methods: {
    subtract() {
      this.result = this.operand1 - this.operand2;
    },
    multi(op1, op2) {
      this.result = op1 * op2;
    },
    divide(op1, op2) {
      this.result= Math.floor(op1 / op2);
    },
    pow(op1, op2) {
      this.result = Math.pow(op1, op2)
    },
    onFocus() {
      console.log('onFocus');
    },
    onKeyUp() {
      console.log('onKeyUp');
    },
    doThan(text, event) {
      console.log(text, event);
    },
  },
};
</script>