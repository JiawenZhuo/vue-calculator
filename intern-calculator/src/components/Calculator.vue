<template>
  <div class="calculator">
      <div class="display">{{current || '0'}}</div>
      <div @click="clear" class="btn">C</div>
      <div @click="sign" class="btn">+/-</div>
      <div @click="percent" class="btn">%</div>
      <div @click="divide" class="btn operator">/</div>
      <div @click="append('7')" class="btn" >7</div>
      <div class="btn" @click="append('8')">8</div>
      <div class="btn" @click="append('9')">9</div>
      <div @click="times" class="btn operator">*</div>
      <div class="btn" @click="append('4')">4</div>
      <div class="btn" @click="append('5')">5</div>
      <div class="btn" @click="append('6')">6</div>
      <div @click="minus" class="btn operator">-</div>
      <div class="btn" @click="append('1')">1</div>
      <div class="btn" @click="append('2')">2</div>
      <div class="btn" @click="append('3')">3</div>
      <div @click="plus" class="btn operator">+</div>
      <div class="btn zero" @click="append('0')">0</div>
      <div class="btn" @click="dot">.</div>
      <div @click="equal" class ="btn">=</div>
    
  </div>
</template>

<script>
export default {
  data(){
    return{
      previous:'',
      current: '444',
      operator: null,
      operatorClicked: false
    }
  },
  methods:{
    clear(){
      this.current = ''
    },
    sign(){
      this.current = this.current.charAt(0) === "-"?
      this.current.slice(1) : `-${this.current}`;
    },
    percent(){
      this.current = `${parseFloat((this.current)/100)}`
    },
    append(number){
      if(this.operatorClicked){
        this.current = '';
        this.operatorClicked = false; 
      }
      this.current = `${this.current}${number}`;
    },
    dot(){
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious(){
      this.previous = this.current;
      this.operatorClicked = true;  
    },
    divide(){
      this.operator = (a, b)=> a/b;
      this.setPrevious();
    },
    plus(){
      this.operator = (a, b)=> a+b; 
      this.setPrevious();  
    },
    miuns(){
      this.operator = (a, b)=> a-b;
      this.setPrevious();
    },
    times(){
      this.operator = (a, b)=> a*b;
      this.setPrevious();
    },
    equal(){
      this.current = `${this.operator(parseFloat(this.current),parseFloat(this.previous))}`;
      this.previous = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .calculator{
    width: 400px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(4, 1fr) ;
    grid-auto-rows: minmax(50px, auto)
  }

  .display{
    grid-column:1/5 ;
    background-color: red;
  }
  .zero{
    grid-column: 1/3;
  }
  .btn{
    background-color: #eeee;
    border: 1px solid #999;

  }

  .operator{
    background-color: orange;
    color: white;
  }
</style>

