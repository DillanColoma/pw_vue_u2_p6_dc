<template>
  <h1 v-if="!pokemonCorrecto">Por favor espere..............</h1>
  <div v-else>
    <h1>Selecciona el Pokemon Correcto</h1>
    <PokemonImagen :idPokemon="pokemonCorrecto.id" :mostrarPokemon="mostrar" />
    <div v-if="!ocultarOpciones">
      <PokemonOpciones
        :pokemons="arreglo"
        @seleccionPokemon="revisarRespuesta($event)"
      />
    </div>
    <div v-else>
        felicidades seleccionaste el pokemon correcto
        
    </div>
  </div>
  
</template>

<script>
import PokemonImagen from "../components/PokemonImagen.vue";
import PokemonOpciones from "../components/PokemonOpciones.vue";
import obtenerPokemonsFachada from "../clientes/ClientePokemonAPI";
export default {
  data() {
    return {
      arreglo: [],
      pokemonCorrecto: null,
      mostrar: false,
      ocultarOpciones: false,
    };
  },
  components: {
    PokemonImagen,
    PokemonOpciones,
  },
  methods: {
    async cargaInicial() {
      /*Llamo por primera ves a mi metodo para que me de las opciones*/
      const vectorInicial = await obtenerPokemonsFachada(7);
      this.arreglo = vectorInicial;

      //Selecion aleatoria de cual es el correcto
      const indice = Math.floor(Math.random() * 7);
      this.pokemonCorrecto = this.arreglo[indice];
    },

    revisarRespuesta(dato) {
      console.log("Se emitio un evento desde el hijo");
      console.log(dato);

      if (dato.ident === this.pokemonCorrecto.id) {
        this.mostrar = true;
        this.ocultarOpciones = true;
      } else {
        console.log("Error........");
        /*Cuando seleccione el pokemon correcto ocultar todas las opciones y que salga
        felicitaciones a selecionado el pokemon correcto*/
      }
    },
  },
  /*Montar el componente en la pagina web,
    los metodos del ciclo de vida no necesitan el await */
  mounted() {
    this.cargaInicial();
  },
};
</script>

<style>
</style>