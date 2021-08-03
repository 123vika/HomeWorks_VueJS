<template>
  <div class="calc">
    {{ message }}
    <div class="input-operand">
      <input
        autofocus
        type="number"
        placeholder="Operand 1"
        @focus="onFocus"
        v-model.number.lazy="operand1"
        key="operand1"
      />
      <br />
      <input
        type="number"
        placeholder="Operand 2"
        @focus="onFocus"
        v-on:keyup="onKeyUp"
        v-model.number.lazy="operand2"
        key="operand2"
      />
      <br />
      <br />
      = {{ result }}
    </div>
    <br />
    <div v-show="error" :class="{ error: !!error }">Error: {{ error }}</div>

    <div class="keyboard">
      <button
        v-for="operation in operations"
        :key="operation"
        @click="calculate(operation)"
        :title="operation"
      >
        {{ operation }}
      </button>
    </div>
    <br />
    <br />

    <div class="checkbox">
      <input type="checkbox" v-model="checked" />
      <label> Отобразить экранную клавиатуру</label>
    </div>

    <div class="array" v-show="checked">
      <button
        v-for="(item, index) in myCollection"
        :key="`${index}_list`"
        @click="onClickNumber(item)"
      >
        {{ item }}
      </button>
      <button @click="onClickDelete">delete</button>
    </div>
    <br />

    <br />

    <div class="rabio-buttons">
      <input
        type="radio"
        id="operand1"
        value="Оperand1"
        name="operand"
        v-model="activeOperand"
      />
      <label for="operand1">Operand1</label>
      <input
        type="radio"
        id="operand2"
        value="Operand2"
        name="operand"
        v-model="activeOperand"
      />
      <label for="operand2">Operand2</label>
    </div>
    <br />
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data: () => ({
    message: "Hello Calculator!",
    operand1: "",
    operand2: "",
    result: 0,
    error: "",
    myCollection: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
    operations: ["+", "-", "*", "/", "*n"],
    checked: "",
    activeOperand: "Operand1",
  }),
  methods: {
    calculate(operation = "+") {
      this.error = "";
      switch (operation) {
        case "+":
          this.sum();
          break;
        case "-":
          this.subtract();
          break;
        case "*":
          this.multi();
          break;
        case "/":
          this.divide();
          break;
        case "*n":
          this.pow();
          break;
      }
    },
    sum() {
      this.result = Number(this.operand1) + Number(this.operand2);
    },
    subtract() {
      this.result = Number(this.operand1) - Number(this.operand2);
    },
    multi() {
      this.result = Number(this.operand1) * Number(this.operand2);
    },
    divide() {
      const { operand1, operand2 } = this;
      if (operand2 === 0 || !operand2) {
        this.error = "На 0 делить нельзя";
      } else {
        this.result = Number(operand1) / Number(operand2); //Math.floor(operand1 / operand2);
      }
    },
    pow() {
      this.result = Math.pow(Number(this.operand1), Number(this.operand2));
    },
    onFocus(event) {
      this.activeOperand = event.target.placeholder.replace(' ', '');
    },
    onKeyUp() {
      console.log("onKeyUp");
    },
    onClickNumber(item) {
      console.log(this.activeOperand);
      if (this.activeOperand === "Оperand1") {
        this.operand1 += item;
      } else {
        this.operand2 += item;
      }
    },
    onClickDelete() {
      if (this.activeOperand === "Оperand1") {
        this.operand1 = this.operand1.slice(0, this.operand1.length - 1);
      } else {
        this.operand2 = this.operand2.slice(0, this.operand2.length - 1);
      }
    },
  },
};
</script>

<style scoped lang='scss'>
.error {
  color: red;
}
.strange-message {
  color: dodgerblue;
  margin-bottom: 20px;
}
</style>