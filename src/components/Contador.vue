<template>
  <h2>{{ presentar }}</h2>
  <!--<p>{{ numero }} <sup>2</sup>={{ calcularCuadrado() }}</p>  LLAMADA A UN METODO-->
  <p>{{ numero }}<sup>2</sup>={{ calcular }}</p>

  <div>
    <button v-on:click="incrementar">+1</button>
    <button v-on:click="disminuir">-1</button>
  </div>
  </template>
  
  <script>
  /*import Contador from './components/Contador.vue';
  
  export default {
    name: 'App',
    components: {
      Contador
    }
  }*/
  export default{
  
    //props:["titulo","num"], Forma básica de declarar un prop.
    props:{
      titulo:  String,
      num: {
        type: Number,
        required:false, //Este siempre va
        default:10,
        validator(value){
          ///////Toda la porgramación
          return  value>0;

        }
      }
    },
    data(){
      return{
        /*propiedades reactivas*/
        numero:this.num,
      };
    },
    methods:{
      calcularCuadrado(){
        console.log("Ingreso al método");
        return(
          this.numero*this.numero
        );/*Usar siempre el this, en html no es necesario*/
      },
      calcularCuadrado2(num1, num2){
        console.log("Ingreso al método 2");
        return num1*num2
      },
      incrementar(){
        this.numero ++;
        /*this.calcular() Esto no es necesrio ya que lo nceseario es
        lo que declara la propiedad computada*/
      },
      disminuir(){
        this.numero --;
      },
  
    },
    computed:{
      calcular(){
        console.log("Ingreso a la propiedad computada");
        return this.numero *this.numero;
      },
      presentar(){
        if(this.titulo!==undefined){
          return this.titulo;
        }else{
          return"Texto que quiero";
  
        }
      }
    },
  
  };
  </script>
  
  <style>
  * {
    background: rgb(255, 246, 80);
  }
  button {
    background: rgb(155, 208, 9);
    border-radius: 5px;
    border: 1px solid white;
    color: rgb(255, 255, 255);
    margin: 5px 5px;
    padding: 5px 20px;
    cursor: pointer;
  }
  
  button:hover {
    background: #5aa67b;
  }
  </style>
  