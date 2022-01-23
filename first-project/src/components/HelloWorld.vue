<template>
  <div class="hello">
    <h1>{{ result }}</h1> 

    <input type="text" v-model.trim.number="operand1"/>
    <input type="text" v-model.trim.number="operand2" @keyup="changeDisabled"/>

    <hr/>
    <button @click="result = operand1 + operand2">+</button>
    <button @click="result = operand1 - operand2">-</button>
    <button @click="divide" :disabled="disabled">/</button>
    <button @click="multiply(operand1, operand2)">*</button>
    <button @click="exponentiation">^</button>
    <button @click="devideInt" :disabled="disabled">\</button>
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
      disabled: false,
      operand1: 0,
      operand2: 0,
      result: 0,
    }
  },
  methods: {
    divide() {
      this.result = this.operand1 / this.operand2;
    },
    multiply(op1, op2) {
      this.result = op1 * op2;
    },
    exponentiation() {
       this.result = this.operand1 ** this.operand2;
    },
    devideInt() {
      this.result = Math.floor(this.operand1 / this.operand2);
    },
    changeDisabled() {
      if(this.operand2 === 0) {
        this.disabled = true;
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
