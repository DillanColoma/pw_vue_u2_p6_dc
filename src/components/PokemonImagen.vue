<template>
  <div class="pokemon-container">
    <img
      v-show="mostrarPokemon"
      :src="imagenFuente"
      alt="No se pudo visualizar la imagen"
    />
    <img
      v-show="!mostrarPokemon"
      class="oculta-pokemon"
      :src="imagenFuente"
      alt="No se pudo visualizar la imagen"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      mostrar: false,
    };
  },
  props: {
    idPokemon: {
      type: Number,
      required: true,
    },
    mostrarPokemon: {
      type: Boolean,
      required: true,
      default: false,
    },
  },
  /*Propiedad computada*/
  computed: {
    imagenFuente() {
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.idPokemon}.svg`;
    },
  },
};
</script>

<style>
.oculta-pokemon {
  filter: brightness(0);
}
img {
  height: 220px;
  width: 200px;
  position: absolute;
  /*right: 37%;*/
  
  /*Se aplica el estilo*/
}
.pokemon-container {
  height: 300px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>