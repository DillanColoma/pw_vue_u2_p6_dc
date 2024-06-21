<template>
    <h1>Selecciona el Pokemon Correcto</h1>
 <PokemonImagen :idPokemon="649" :mostrarPokemon="false"/>
 <PokemonOpciones :pokemons="arreglo"/>
</template>

<script>
import PokemonImagen from '../components/PokemonImagen.vue';
import PokemonOpciones from '../components/PokemonOpciones.vue'
import obtenerPokemonsFachada from '../clientes/ClientePokemonAPI'
export default {
    data(){
     return{
        arreglo:[]
     }
    },
    components:{
        PokemonImagen,
        PokemonOpciones
    },
    methods:{
        async cargaInicial(){
            /*Llamo por primera ves a mi metodo para que me de las opciones*/
            const vectorInicial= await obtenerPokemonsFachada(4);
            this.arreglo= vectorInicial;
        }
    },
    /*Montar el componente en la pagina web,
    los metodos del ciclo de vida no necesitan el await */
    mounted(){
        this.cargaInicial();

    }
}
</script>

<style>

</style>