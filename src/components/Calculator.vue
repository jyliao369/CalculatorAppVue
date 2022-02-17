<template>
  <div class="container">
    <div class="calculator">
      <div class="display">{{ current }}</div>
      <button @click="clear">C</button>
      <button @click="sign">+/-</button>
      <button @click="percent">%</button>
      <button @click="operator('÷')" class="operator">÷</button>
      <button @click="append('7')">7</button>
      <button @click="append('8')">8</button>
      <button @click="append('9')">9</button>
      <button @click="operator('×')" class="operator">×</button>
      <button @click="append('4')">4</button>
      <button @click="append('5')">5</button>
      <button @click="append('6')">6</button>
      <button @click="operator('-')" class="operator">-</button>
      <button @click="append('1')">1</button>
      <button @click="append('2')">2</button>
      <button @click="append('3')">3</button>
      <button @click="operator('+')" class="operator">+</button>
      <button @click="append('0')" class="zero">0</button>
      <button @click="dot()">.</button>
      <button @click="calculate()" class="operator">=</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: "0",
      opOn: false,
    };
  },
  methods: {
    clear() {
      this.current = "0";
    },
    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      this.current =
        this.current === "0" ? `${number}` : `${this.current}${number}`;
      this.opOn = false;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    operator(operator) {
      if (this.opOn === false) {
        this.current = `${this.current}${operator}`;
        this.opOn = true;
      } else {
        this.current = `${this.current.substr(
          0,
          this.current.length - 1
        )}${operator}`;
      }
    },
    calculate() {
      let convEq = this.current.replaceAll("÷", "/").replaceAll("×", "*");
      this.current = eval(convEq);
    },
  },
};
</script>

<style scoped>
body {
  margin: 0px;
}
.container {
  display: flex;
  justify-content: center;
}
.display {
  grid-column: 1/5;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  background: gray;
  color: white;
  border: 1.5px solid #333;
}
.calculator {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  width: 500px;
  font-size: 25px;
}
button {
  border: 1.5px solid #333;
  font-size: 25px;
}
.zero {
  grid-column: 1/3;
}
.operator {
  background: orange;
}
</style>
