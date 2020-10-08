<template>
  <div id="app">
    <div class="container">
      <div class="calculator">
        <div class="card">
          <div class="card-header">
            <div class="col">
              <h1>Casio</h1>
            </div>
          </div>
          <div class="card-body">
            <div class="row">
              <Display :showdisplay="showdisplay" />
            </div>
            <div class="numpad">
              <Numpad @onButtonValue="showValue" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Display from "./components/Display";
import Numpad from "./components/Numpad";
export default {
  name: "App",
  data() {
    return {
      showdisplay: "",
      accumulator: "",
      lastestValue: "",
      operation: [],
    };
  },
  components: {
    Display,
    Numpad,
  },
  methods: {
    showValue(value) {
      if (value == "=") {
        this.accumulator = this.calculate(this.operation[0]);
        this.lastestValue=''
        this.showdisplay = this.accumulator;
      } else if (value == "%") {
        this.specialOpearation(value)
      } else if (value == "C") {
        this.clear()
      }else if(value == "√"){
        this.specialOpearation(value)
      } else if (this.operation.length == 0) {
        this.setdataValue(value,'accumulator')
      } else if (this.operation.length == 1) {
        this.setdataValue(value,'lastesValue')
      } else {
        this.showdisplay += value;
        this.accumulator = this.calculate(this.operation[0]);
        this.lastestValue = "";
        this.lastestValue += value;
      }
    },
    calculate(type) {
      const acc = parseInt(this.accumulator);
      const lastest = parseInt(this.lastestValue);
      this.operation.shift()
      switch (type) {
        case "+":
          return acc + lastest;
        case "-":
          return acc - lastest;
        case "*":
          return acc * lastest;
        case "/":
          return acc / lastest;
        case "%":
          return acc / 100;
        case "√":
           return Math.sqrt(acc)
        default:
          return;
      }
      
    },
    clear(){
        this.showdisplay = "";
        this.accumulator = "";
        this.lastestValue = "";
        this.operation = [];
    },
    specialOpearation(value){
      if(this.lastestValue!=""){
          this.showdisplay='ERROR'
        }else{
          this.accumulator = this.calculate(value);
          this.showdisplay = this.accumulator;
    }
    },
     setdataValue(value,targetstate){
         if (typeof value == "string" && value != ".") {
          this.operation.push(value);
          this.showdisplay += value;
        } else {
          this.showdisplay += value;
          if(targetstate=='accumulator'){
            this.accumulator+= value;
          }else{
            this.lastestValue+= value;
          }
        }
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.calculator {
  width: 50%;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.numpad {
  margin-top: 20px;
}
</style>
