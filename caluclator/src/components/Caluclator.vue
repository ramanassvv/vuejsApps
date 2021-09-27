<template>
  <div class="calculator">
    <div class= "container">
      <div class="display">{{current || '0'}}</div>
      <div class="row"> 
        <div @click="clear" class="btn">AC</div>
          <div @click="sign" class="btn">+/-</div>
          <div @click="percent" class="btn">%</div>
          <div @click="handleOperator('÷')" class="btn operator">÷</div>
      </div>
      <div class="row"> 
        <div @click="append('7')" class="btn">7</div>
        <div @click="append('8')" class="btn">8</div>
        <div @click="append('9')" class="btn">9</div>
        <div @click="handleOperator('x')" class="btn operator">x</div>
      </div>
      <div class="row"> 
        <div @click="append('4')" class="btn">4</div>
        <div @click="append('5')" class="btn">5</div>
        <div @click="append('6')" class="btn">6</div>
        <div @click="handleOperator('-')" class="btn operator">-</div>
      </div>
      <div class="row"> 
        <div @click="append('1')" class="btn">1</div>
        <div @click="append('2')" class="btn">2</div>
        <div @click="append('3')" class="btn">3</div>
        <div @click="handleOperator('+')" class="btn operator">+</div>
      </div>
      <div class="row">
        <div @click="append('0')" class="btn zero">0</div>
        <div @click="dot" class="btn">.</div>
        <div @click="handleOperator('=')" class="btn operator">=</div>
      </div>
    </div>
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
    }
  },
  methods: {
    clear() {
      this.current = ''
      this.previous = null
      this.operator = null
      this.clickedOperator = false
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ? 
        this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.clickedOperator) {
        this.clickedOperator = false
        this.current = number
      } else {
        this.current = this.current === '0' ? number : `${this.current}${number}`
      }
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    handleOperator (newOperator) {
      const numberValue = parseFloat(this.current)
      if (this.operator && this.clickedOperator) {
        this.operator = newOperator
      }
      if (this.previous == null) {
        this.previous = numberValue
      } else if (this.operator) {
        const result = this.calculate(this.previous, numberValue, this.operator)
        this.current = String(result)
        this.previous = result
      }
      this.clickedOperator = true
      this.operator = newOperator
    },
     calculate (first, second, operator) {
      switch (operator) {
        case '+':
          return first + second
        case '-':
          return first - second
        case 'x':
          return first * second
        case '÷':
          return first / second
        default:
          return second
      }
    }
  }
}
</script>


<style scoped>
.calculator {
   margin: 2rem 0;
}

.container {
   width: 40%;
   padding: 1rem;
   border-radius: 36px;
   background:#0d1a36;
}
.display {
   padding: 2rem;
   display: flex;
   justify-content: flex-end;
   color: white;
   font-size: 2rem;
}

.row {
  display: flex;
  justify-content: center;
  flex-direction: row;
  align-items: space-around;
}

.btn {
  display: flex;
  justify-content: center;
  align-items: center;
  appearance: none;
  margin: .5rem .5rem;
  width: 15.9px;
  min-width: 35.9px;
  padding: 1.24rem 0.91rem ;
  border-radius: 2rem;
  background-color:#273344;
  color: white;
  font-size: 1rem;
}

.operator {
  color:orange;
  font-size: 1rem;
}
.zero {
  width: 7rem;
}

.btn:hover {
  cursor: pointer;
}
</style>
