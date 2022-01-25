<template>
  <div class="hello">
    <h1>{{ result }}</h1> 

    <div class="display">
      <input v-model.number="operand1" />
      <input v-model.number="operand2" />
    </div>
    <hr/>
    <button v-for="(operand, idx) in operands" @click="calculate(operand)" :key="idx">{{ operand }}</button>
    <hr/>
    <input type="checkbox" id="checkbox" v-model="checked">
    <label for="checkbox">Отобразить экранную клавиатуру</label>
    <br>
    <div v-if="checked">
      <button v-for="(button, idx) in buttons" @click="display(button)" :key="idx">{{ button }}</button>
      <br>
      <input type="radio" id="one" value="1" v-model="picked">
      <label for="one">Операнд 1</label>
      <input type="radio" id="two" value="2" v-model="picked">
      <label for="two">Операнд 2</label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      operand1: 0,
      operand2: 0,
      result: 0,
      error: '',
      operands: ['+', '-', '*', '/', '^', '%'],
      checked: false,
      buttons: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '←'],
      picked: '1',
      fibResult: 0,
    }
  },
  methods: {
    calculate(operation="+") {
      this.error = "";
      switch (operation) {
        case "+":
          this.add();
          break;
        case "-":
          this.substract();
          break;
        case "*":
          this.multiply();
          break;
        case "/":
          this.divide();
          break;
        case "^":
          this.exponentiation();
          break;
        case "%":
          this.devideInt();
          break;
      }
    },
    add() {
      this.result = this.operand1 + this.operand2;
      this.fibResult = this.fibb1 + this.fibb2;
    },
    substract() {
      this.result = this.operand1 - this.operand2;
      this.fibResult = this.fibb1 - this.fibb2;
    },
    divide() {
      if ( this.operand2 === 0 ) {
        this.error = "На 0 делить нельзя";
        return;
      }
      this.result = this.operand1 / this.operand2;
    },
    multiply() {
      this.result = this.operand1 * this.operand2;
    },
    exponentiation() {
       this.result = this.operand1 ** this.operand2;
    },
    devideInt() {
      if ( this.operand2 === 0 ) {
        this.error = "На 0 делить нельзя";
        return;
      }
      this.result = Math.floor(this.operand1 / this.operand2);
    }, 
    display(button) {
      switch(this.picked) {
        case "1":
          if (button === "←") {
            this.operand1 = Math.floor(this.operand1 / 10);
          }
          else {
            this.operand1 += button;
          }
          break;
        case "2":
          if (button === "←") {
            this.operand2 = Math.floor(this.operand2 / 10);
          }
          else {
            this.operand2 += button;
          }
          break;
      }
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
