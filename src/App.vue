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
              <Numpad 
              @appendNumber="handleNumber" 
              @appendOperation="handleOperation"
              />
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
    handleOperation(operation){
      switch(operation){
        case '=':
          this.equal()
          break
        case'C':
           this.clear()
           break
        case'√':
        case'%':
          this.specialOpearation(operation)
            break
        default:
          this.otherOperation(operation)
      }
    },
    handleNumber(number){
        if(this.operation.length==0){
          this.showdisplay+=number
          this.accumulator+=number
        }else{
          this.showdisplay+=number
          this.lastestValue+=number
        }
    },
    calculate(operation) {
      const acc = parseFloat(this.accumulator);
      const lastest = parseFloat(this.lastestValue);
      this.lastestValue=''
      this.operation.shift()
      switch (operation) {
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
    otherOperation(operation){
          this.operation.push(operation)
          this.showdisplay+=operation
          if(this.operation.length>1){
              this.accumulator=this.calculate(this.operation[0])
            }
    },
    clear(){
        this.showdisplay = "";
        this.accumulator = "";
        this.lastestValue = "";
        this.operation = [];
    },
    equal(){
        this.accumulator = this.calculate(this.operation[0]);
        this.showdisplay = `${this.accumulator}`;
    },
    specialOpearation(operation){
      if(this.lastestValue!=""||this.accumulator==""){
          this.showdisplay='ERROR'
        }else{
          this.accumulator = this.calculate(operation);
          this.showdisplay = `${this.accumulator}`;
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
