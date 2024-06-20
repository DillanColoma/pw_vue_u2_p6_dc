<template>
  <img v-if="img"
    v-bind:src="img"
    alt="No se pudo"
  />
  <div class="oscuro"></div>
  <div class="pregunta-container">
    <input v-model="pregunta" type="text" placeholder="Hazme una pregunta" />
    <p>Recuerda terminar la pregunta con el signo de interrogación (?)</p>

    <div v-show="mensaje" class="respuesta">
      <h2>{{pregunta}}</h2>
      <h1>{{ respuesta==='yes'?'SI!':'NO!' }}</h1>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      /*aqui se declara las propiedades reactivas*/
      pregunta:null,
      respuesta:null,
      img:null,
      mensaje:false
    }
  },
  /*Option Api obsevador*/
  watch:{
      pregunta(value,oldvalue){
        this.mensaje=false;
        /*Primer elemento pongo el value donde me da el valor actual 
        y el segundo argumento el oldvalue que me da el valor antiguo */
        console.log({value,oldvalue});
        if(!value.includes('?')){
          return /*Salgase del observador*/;
          
        }
        //Consumir el Api para obtener la respuesta.
        this.obtenerRespuesta();
        this.mensaje=true;

      },
  },
  methods:{
   async obtenerRespuesta(){
          this.respuesta="Pensando......."
          /*Para consumo de Apis Vue para consumo web maneja un verbo o
          metodos HTTP, son tipos de request */
          /*SOLO RECIBE PETICIONES GET
          recibe como argumento la URL del API
          .then(resp => resp.json())
          await espera q la Api responda*/
          const data=await fetch('https://yesno.wtf/api').then(r=>r.json())
          console.log(data);
          const{answer,forced, image}=data;
          console.log(answer);
          this.respuesta=answer;
          this.img=image;
          return data;
    },
    async prueba(){
      const data2=await this.obtenerRespuesta();
    },
  },
};
</script>

<style scoped>/*Se garantiza que los estilos solo sean de un solo componente*/ 
img, .oscuro{
  max-height: 100%;
  height: 100vh;
  max-width: 100%;
  width: 100vw;
  position: fixed;
  
  top: 0px;
  left: 0px; 
}
.oscuro{
  background-color: rgba(0, 0, 0, 0.6);
  /* 0.0 es full transparente
     1.0 es full opaco */
}
.pregunta-container{
  position: relative;/* A lo que ponemos relativa, independientemente de los elementos que existan 
                        siempre van a estar primero, que esten encima */
                        
}
input{
  margin-top: 80px;
  width: 360px;
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  /*text-align: center;*/
 
}
input:focus{
  outline: none;
}
p,h1,h2{
  color: aliceblue;
}
p{
  font-size: 25px;
  margin-top: 0px ;/*Para que mi p se pegue a mi input */

}
.respuesta{
  margin-top: 125px;
}
body{
  background-color: black;
}
</style>