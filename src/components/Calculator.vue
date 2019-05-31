<template>
  <div class="calculator">
    <div class="display">{{ current || '0'}}</div>
    <div class="btn" @click="clear">C</div>
    <div class="btn" @click="sign">+/-</div>
    <div class="btn"  @click="percent()">%</div>
    <div class="btn operator" @click="divide">÷</div>
    <div class="btn" @click="append('7')">7</div>
    <div class="btn" @click="append('8')">8</div>
    <div class="btn" @click="append('9')">9</div>
    <div class="btn operator" @click="times">x</div>
    <div class="btn" @click="append('4')">4</div>
    <div class="btn" @click="append('5')">5</div>
    <div class="btn" @click="append('6')">6</div>
    <div class="btn operator" @click="minus">-</div>
    <div class="btn" @click="append('1')">1</div>
    <div class="btn" @click="append('2')">2</div>
    <div class="btn" @click="append('3')">3</div>
    <div class="btn operator" @click="add">+</div>
    <div  class="btn zero" @click="append('0')">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn operator" @click="equal">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
      equalClicked: false,
      currentStock: '',
    }
  },
  methods: {
    clear() {
      this.current = '';
      this.previous = null;
      this.current = '';
      this.operator = null;
      this.operatorClicked = false;
      this.equalClicked = false;
      this.currentStock = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ?
        this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      if (this.current !== '') {
        this.current = `${parseFloat(this.current) / 100}`;
      }
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      if (this.equalClicked) {
        this.current = '';
        this.previous = '';
        this.currentStock = '';
        this.equalClicked = false;
      }
      this.current = `${this.current + number}`;
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => {
        console.log(b);
        let calc_result;
        if (b === 0) {
          calc_result = '0'
          console.log(calc_result);
        } else {
          calc_result = a / b;
        }
        console.log(calc_result);
        return calc_result;
      }
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {

      if (this.equalClicked) {
        this.current = `${this.operator(
          parseFloat(this.current),
          parseFloat(this.currentStock)
        )}`;
      } else {
        this.currentStock = this.current
        this.current = `${this.operator(
          parseFloat(this.previous),
          parseFloat(this.current)
        )}`;
        this.equalClicked = true;
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .calculator {
    margin: 0 auto;
    width: 400px;
    font-size: 40px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
  }

  .display {
    grid-column: 1 / 5;
    background-color: #333;
    color: white;
  }

  .zero {
    grid-column: 1 / 3;
  }

  .btn {
    background-color: #F2F2F2;
    border: 1px solid #999;
  }

  .operator {
    background-color: orange;
    color: white;
  }
</style>
