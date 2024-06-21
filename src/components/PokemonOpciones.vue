<template>
  <div class="opciones-container">
    <ul>
      <li v-for="pokemon in pokemons" :key="pokemon.id">{{ pokemon.name }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    pokemons: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style>
ul {
  list-style-type: none; /**le quito las viñetas */
}
li {
  border: 1px solid rgba(0, 0, 0, 0.5);
  border-radius: 5px;
  margin-bottom: 20px;
  width: 250px;
  background: white;
  cursor: pointer;
}

li:hover {
  background: rgba(0, 0, 0, 0.3);
}
.opciones-container {
  display: flex;
  justify-content: center;
}
</style>