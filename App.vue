<template>
  <div>
    <table class="table">
      <tbody>
        <tr>
          <td>Pokemon</td>
          <td>Imagen</td>
        </tr>
        <tr v-for="pokemon in pokemons" :key="pokemon.name">
          <td class="celd">{{ pokemon.name }}</td>
          <td class="celd"><img :src="pokemon.img" /></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      todos: null,
      pokemons: [],
    };
  },

  mounted() {
    this.getTodos();
  },

  methods: {
    getTodos() {
      let promiseArray = [];
      for (let index = 1; index < 13; index++) {
        promiseArray.push(axios(`https://pokeapi.co/api/v2/pokemon/${index}`));
      }
      Promise.all(promiseArray).then((response) =>
        response.map((r) =>
          this.pokemons.push({
            name: r.data.forms[0].name,
            img: r.data.sprites.front_default,
          })
        )
      );
    },
  },
};
</script>

<style scoped>
.table {
  border: 2px solid;
  margin: 0 auto;
  text-align: center;
}
.celd {
  background: #eaeaea;
  border: 2px solid;
}
</style>
>
