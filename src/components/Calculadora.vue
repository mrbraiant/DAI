<template>
  <div class="calculadora">
    <div class="botao cabecalho">Calculadora do Braiant(Atv 3)</div>
    <div class="display">{{current || '0'}}</div>
    <div @click="clear" class="botao">C</div>
    <div @click="sign" class="botao">+/-</div>
    <div @click="percent" class="botao">%</div>
    <div @click="divide" class="botao operador">/</div>
    <div @click="append('7')" class="botao">7</div>
    <div @click="append('8')" class="botao">8</div>
    <div @click="append('9')" class="botao">9</div>
    <div @click="multiplica" class="botao operador">x</div>
    <div @click="append('4')" class="botao">4</div>
    <div @click="append('5')" class="botao">5</div>
    <div @click="append('6')" class="botao">6</div>
    <div @click="menos" class="botao operador">-</div>
    <div @click="append('1')" class="botao">1</div>
    <div @click="append('2')" class="botao">2</div>
    <div @click="append('3')" class="botao">3</div>
    <div @click="soma" class="botao operador">+</div>
    <div @click="append('0')" class="botao zero">0</div>
    <div @click="ponto" class="botao">.</div>
    <div @click="igual" class="botao operador">=</div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods:{
    clear(){
      this.current = "";
    },
    sign(){
      this.current = this.current.charAt(0) === '-' ?
      this.current.slice(1) : `-${this.current}`;
    },
    percent(){
      this.current = `${parseFloat(this.current) / 100}`
    },
    append(number){
      if (this.operatorClicked){
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`
    },
    ponto(){
      if (this.current.indexOf('.') === -1){
        this.append('.');
      }
    },
    setPrevious(){
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide(){
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    multiplica(){
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    menos(){
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    soma(){
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    igual(){
       this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
        )}`;
        this.previus = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculadora{
  margin: 0 auto;
  width: 400px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display{
  grid-column: 1 / 5;
  background-color: black;
  color: white;

}
.zero{
  grid-column: 1/3;
}
.botao{
  background-color: white;
  border: 1px solid #999;
}
.operador{
  background-color: orange;
  color: white;
}
.cabecalho{
  grid-column: 1/5;
  background-color: gray;
  color: white;
}

</style>
