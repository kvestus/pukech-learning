<template>
  <div class="calculator">
    <div class="display noselect">{{current || '0'}}</div>
    <div @click="clear"  class="btn signW noselect">C</div>
    <div @click="sign" class="btn signW noselect">+/-</div>
    <div @click="percent" class="btn signW noselect">%</div>
    <div @click="divide" class="btn operator noselect">÷</div>
    <div @click="append('7')" class="btn noselect">7</div>
    <div @click="append('8')" class="btn noselect">8</div>
    <div @click="append('9')" class="btn noselect">9</div>
    <div @click="times" class="btn operator noselect">x</div>
    <div @click="append('4')" class="btn noselect">4</div>
    <div @click="append('5')" class="btn noselect">5</div>
    <div @click="append('6')" class="btn noselect">6</div>
    <div @click="minus" class="btn operator noselect">-</div>
    <div @click="append('1')" class="btn noselect">1</div>
    <div @click="append('2')" class="btn noselect">2</div>
    <div @click="append('3')" class="btn noselect">3</div>
    <div @click="add" class="btn operator noselect">+</div>
    <div @click="append('0')"  class="btn zero noselect">0</div>
    <div @click="dot" class="btn noselect">.</div>
    <div @click="equal" class="btn operator noselect">=</div>

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
    };
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-'
        ? this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
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
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous),
      )}`;
      this.previous = null;
    },
  },
  name: 'Calculator',
  props: {
    msg: String,
  },

};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator{
  background-color: black;
  margin: 0 auto;
  width: 290px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr) ;
  grid-auto-rows: minmax(50px, auto);
}

.display{
  text-align: right;
  padding-right: 8px;
  grid-column: 1 / 5;
  background-color: black;
  color: white
}

.zero{
  grid-column: 1/3;
}

.btn{
  background-color: #3c3c3c;
  color: white;
  padding: 20px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 20px;
  margin: 6px 4px;
  border-radius: 50px;
  cursor: pointer;
  tasition: all .3s linear;
  -webkit-transition:  all .3s linear;
  -moz-transition:  all .3s linear;
  text-transform: uppercase;
}

.btn:hover {
  background-color: #787878;
  color: white;
  tasition: all .3s linear;
  -webkit-transition:  all .3s linear;
  -moz-transition:  all .3s linear;
}

.operator{
  background-color: orange;
  color: white;
}
.operator:hover {
  background-color: #fc9;
  color: white;
  tasition: all .3s linear;
  -webkit-transition:  all .3s linear;
  -moz-transition:  all .3s linear;
}

.signW{
  background-color: #cccccc;
  color: black;
}
.signW:hover {
  background-color: #ffffff;
  color: black;
  tasition: all .3s linear;
  -webkit-transition:  all .3s linear;
  -moz-transition:  all .3s linear;
}

.noselect{
  color: #white;
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
</style>
