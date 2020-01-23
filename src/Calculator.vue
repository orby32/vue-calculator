<template>
<div>
    <div class="grid-container">
      <div class="result">{{current || '0'}}</div>
      <div @click="append('0')" class="zero">0</div>
      <div @click="dot" class="dot">.</div>
      <div @click="equal" class="equal">=</div>
      <div @click="clearResult" class="AC">AC</div>
      <div @click="sign" class="sign">+/-</div>
      <div @click="percent" class="operator">%</div>
      <div @click="divide" class="operator-2">/</div>
      <div @click="times" class="operator-3">X</div>
      <div @click="minus" class="operator-4">-</div>
      <div @click="add" class="operator-5">+</div>
      <div @click="append('1')">1</div>
      <div @click="append('2')">2</div>
      <div @click="append('3')">3</div>
      <div @click="append('4')">4</div>
      <div @click="append('5')">5</div>
      <div @click="append('6')">6</div>
      <div @click="append('7')">7</div>
      <div @click="append('8')">8</div>
      <div @click="append('9')">9</div>
    </div>
    <div>{{history}}</div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            current: '',
            previous: null,
            operator: null,
            operatorClicked: false,
            history: []
        }
    },
    methods: {
    clearResult() {
        this.current = '';
    },
    setPrevious() {
        this.previous = this.current;
        this.current = '';
    },
    sign() {
        this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`; 
    },
    dot() {
        if (this.current.indexOf('.') === -1) {
            this.append('.');
        }
    },
    percent() {
        this.current = `${parseFloat(this.current) / 100}`;
        },
    append(number) {
        if (this.operatorClicked) {
            this.current = '';
            this.operatorClicked = true;
        }
            this.current = `${this.current}${number}`;
    },
    add() {
        this.operator = (a, b) => a + b;
        this.setPrevious();
    },
    minus() {
        this.operator = (a, b) => a - b;
        this.setPrevious();
    },
    divide() {
        this.operator = (a, b) => a / b;
        this.setPrevious();
    },
    times() {
        this.operator = (a, b) => a * b;
        this.setPrevious();
    },
    equal() {
        this.current = `${this.operator(parseFloat(this.previous), parseFloat(this.current))}`;
        const item = {
            current: this.current,
            operator: this.operator,
            previous: this.previous,
        }
        this.history.push(item);
        this.previous = null;
    }
}
};
</script>

<style scoped>
.grid-container {
  display: grid;
  grid-template-columns: 1fr 1.1fr 0.9fr 1fr;
  grid-template-rows: 2fr 1fr 1fr 1fr 1fr 1fr;
  grid-template-areas: "result result result result" "AC positive-negative operator operator-2" "\31  \32  \33  operator-3" "\34  \35  \36  operator-4" "\37  \38  \39  operator-5" "zero zero dot equal";
  max-width: 50%;
  margin: auto;
  height: 500px;
  border-radius: 2px;
}
.grid-container div {
    border: 1px solid black;
    font-size: 2rem;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    transition: all .3s;
}
.grid-container div:hover {
    opacity: .8;
}
.grid-container div.result {
     cursor: default;
    justify-content: flex-end;
    align-items: flex-end;
    font-size: 4rem;
    padding: 1rem;
     
}
.result { grid-area: result; background-color: rgba(0,0,0,.2);}

.zero { grid-area: zero; }

.dot { grid-area: dot; }

.equal { grid-area: equal; }

.AC { grid-area: AC; }

.sign { grid-area: positive-negative; }

.operator { grid-area: operator; }

.operator-2 { grid-area: operator-2; }

.operator-3 { grid-area: operator-3; }

.operator-4 { grid-area: operator-4; }

.operator-5 { grid-area: operator-5; }

.operator, .operator-2, .operator-3, .operator-4, .operator-5 {
    color: white; 
    background-color: orangered;
}
</style>
