<template>
  <div
    id="app"
    v-on:keyup.c ="limpar()"
    v-on:keyup.+ ="somar()"
    v-on:keyup.* ="multiplicar()"
    v-on:keyup.- ="diminuir() "
    v-on:keyup.d="dividir()"
    v-on:keyup.p="porcento()"
    v-on:keyup.i="resultado()"
  >
    <h1>{{titulo}}</h1>

    <div id="geral">
      <div id="calc">
        <div id="topo">
          <div id="display">{{valorCorrente || "0"}}</div>
        </div>

        <div id="btnOps">
           <button class="ops1" @click="limpar()">C</button>
          <button class="ops1" @click="sinal">+/-</button>
          <button class="ops1" @click="porcento('%')">%</button>
          <button class="ops1" @click="dividir">÷</button>
          <button class="ops" @click="teclas('7')">7</button>
          <button class="ops" @click="teclas('8')">8</button>
          <button class="ops" @click="teclas('9')">9</button>
          <button class="ops1" @click="multiplicar('x')">x</button>
          <button class="ops" @click="teclas('4')">4</button>
          <button class="ops" @click="teclas('5')">5</button>
          <button class="ops" @click="teclas('6')">6</button>
          <button class="ops1" @click="somar">+</button>
          <button class="ops" @click="teclas('1')">1</button>
          <button class="ops" @click="teclas('2')">2</button>
          <button class="ops" @click="teclas('3')">3</button>
          <button class="ops1" @click="diminuir">-</button>
          <button class="ops" @click="teclas('0')">0</button>
          <button class="ops1" @click="ponto">.</button>
          <button class="ops1" id="igual" @click="resultado">=</button>
          
        </div>
      </div>
    </div>
  </div>
</template>

<script>
    export default {
        data() {
            return {
                valorCorrente: "",
                numeroAnterior: "",
                operador: null,
                operadorClicado: false,
                titulo: "Calculadora Vue"
            };
        },
        methods: {
            limpar() {
                this.valorCorrente = "";
            },
            sinal() {
                this.valorCorrente =
                    this.valorCorrente.charAt(0) === "-" ?
                    this.valorCorrente.slice(1) :
                    `-${this.valorCorrente}`;
            },
            //metodo responsavel pela operação porcentagem
            porcento() {
                this.valorCorrente = `${parseFloat(this.valorCorrente) / 100}`;
            },
            //metodo responsavel para inserir numeros
            teclas(numero) {
                if (this.operadorClicado) {
                    this.valorCorrente = "";
                    this.operadorClicado = false;
                }
                this.valorCorrente = `${this.valorCorrente}${numero}`;
            },
            // Método responsável por adicionar 'ponto' no display da Calculadora:
            ponto() {
                if (this.valorCorrente.indexOf(".") === -1) {
                    this.teclas(".");
                }
            },
            setarValor() {
                this.numeroAnterior = this.valorCorrente;
                this.operadorClicado = true;
            },
            // Método responsável por realizar a operação da 'divisão'
            dividir() {
                this.operador = (num1, num2) => (num1 / num2).toFixed(2);
                this.setarValor();
            },
            // Método responsável por realizar a operação da 'multiplicar'
            multiplicar() {
                this.operador = (num1, num2) => (num1 * num2).toFixed(2);
                this.setarValor();
            },
            // Método responsável por realizar a operação da 'diminuir'
            diminuir() {
                this.operador = (num1, num2) => (num1 - num2).toFixed(2);
                this.setarValor();
            },
            // Método responsável por realizar a operação da 'somar'
            somar() {
                this.operador = (num1, num2) => (num1 + num2).toFixed(2);
                this.setarValor();
            },

            // Método responsável por apresentar o resultado das operações da Calculadora:
            resultado() {
                this.valorCorrente = `${this.operador(
        parseFloat(this.numeroAnterior),
        parseFloat(this.valorCorrente)
      )}`;
            }
        }
    };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    * {
        box-sizing: border-box;
        padding: 0;
        margin: 0;
    }
    
    button,
    input {
        outline: 0;
    }
    
    #geral {
        width: 100vw;
        height: 100vh;
        display: flex;
    }
    
    #calc {
        width: 300px;
        background-color: #333;
        position: relative;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        margin: auto;
        padding: 15px;
        border-radius: 10px;
    }
    
    #topo {
        width: 100%;
        height: 100px;
        background-color: #ccc;
        border-radius: 5px;
    }
    
    #display {
        width: 100%;
        height: 100%;
        border: 0;
        border-radius: 25px;
        background-color: transparent;
        text-align: right;
        font-size: 40px;
        margin-bottom: 50px;
        font-family: Arial;
        color: #444;
        padding: 5px;
        display: block;
        overflow-y: scroll;
    }
    
    #btnOps {
        width: 100%;
        margin-top: 10px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        flex-wrap: wrap;
    }
    
    .ops {
        width: 60px;
        height: 60px;
        border-radius: 10px;
        font-size: 30px;
        color: #fff;
        background-color: #555;
        margin: 5px 0;
    }
    
    .ops1 {
        width: 60px;
        height: 60px;
        border-radius: 10px;
        font-size: 30px;
        color: #fff;
        background-color: green;
        margin: 5px 0;
    }
    
    #igual {
        width: 130px;
    }
    
    h1 {
        text-align: center;
        font-weight: bold;
    }
</style>