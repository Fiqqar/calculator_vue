<template>
    <div class="calculator">
        <div class="display">{{ current || "0" }}</div>
            <div @click="clear" class="btn">C</div>
            <div @click="sign()" class="btn">+/-</div>
            <div @click="percentage()" class="btn">%</div>
            <div @click="divide()" class="btn operator">:</div>
            <div @click="append('7')" class="btn">7</div>
            <div @click="append('8')" class="btn">8</div>
            <div @click="append('9')" class="btn">9</div>
            <div @click="multi()" class="btn operator">x</div>
            <div @click="append('4')" class="btn">4</div>
            <div @click="append('5')" class="btn">5</div>
            <div @click="append('6')" class="btn">6</div>
            <div @click="minus()" class="btn operator">-</div>
            <div @click="append('1')" class="btn">1</div>
            <div @click="append('2')" class="btn">2</div>
            <div @click="append('3')" class="btn">3</div>
            <div @click="add()" class="btn operator">+</div>
            <div @click="append('0')" class="btn zero">0</div>
            <div @click="dot()" class="btn">.</div>
            <div @click="equal()" class="btn operator">=</div>
    </div>
</template>

<script>
    export default {
        name: "CalculatorComp",
        data() {
            return {
                previous: null,
                current: "",
                operator: null,
                operatorclick: false
            }
        },
        methods: {
          clear() {
            this.current = "";
          },
          append(num) {
            if(this.operatorclick) {
                this.current = ""
                this.operatorclick = false
            }
            this.current = `${this.current}${num}`
          },
          setprevious() {
            this.previous = this.current;
            this.operatorclick = true
          },
          add() {
            this.operator = (a,b) => a + b
            this.setprevious()
          },
          equal() {
            this.current = `${this.operator(
                parseFloat(this.current),
                parseFloat(this.previous)
            )}`
            this.previous = null
          },
          minus() {
            this.operator = (a,b) => b - a
            this.setprevious()
          },
          multi() {
            this.operator = (a,b) => a * b
            this.setprevious()
          },
          divide() {
            this.operator = (a,b) => a / b
            this.setprevious()
          },
          dot() {
            if (this.current.indexOf('.') === -1) {
              this.append(".")
            }
          },
          percentage() {
            this.current = `${parseFloat(this.current) / 100}`
          },
          sign() {
            this.current = this.current.charAt(0) === '-'?this.current.slice(1) : `-${this.current}`
          }
        }
    }
</script>
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