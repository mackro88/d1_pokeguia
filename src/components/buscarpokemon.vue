<template>
  <div id="finder"> 
    <img id="pokemonlogo" src="https://www.freepnglogos.com/uploads/pokemon-logo-text-png-7.png" alt="Pokémon Logo">
    <h1>Pokeguía</h1>
    <input type="text" v-model="pokeName" @keyup.enter="getData()" placeholder="Escribe un nombre..."/><button @click="getData()">Buscar</button>
    
    <h2>{{capitalize(namePokemon)}}</h2>
    <img :src="imgPokemon" :alt="result.name">
    <h3>Habilidades</h3> 
      <ul v-for="abilities in abilitiesPokemon" :key="abilities.index">    
        <li>{{capitalize(abilities.ability.name)}}</li>
      </ul> 
    <h3>Movimientos</h3>
      <ul v-for="moves in movesPokemon" :key="moves.index">    
        <li>{{capitalize(moves.move.name)}}</li>
      </ul>
  </div>
</template>

<script>
export default {
  name: "BuscarPokemon",
  data:()=>({
    pokeName: "pikachu",
    result: [],
  }),
  computed: {
    namePokemon(){
      return this.result.name
    },
    imgPokemon(){
      return this.result.sprites.front_default   
    }, 
    abilitiesPokemon(){
      return this.result.abilities
    },
    movesPokemon(){
      return this.result.moves
    }
  },
  methods: {
    async getData() {
      try {
        let response = await fetch(`https://pokeapi.co/api/v2/pokemon/${this.pokeName}`);
        this.result = await response.json();
      } catch (error) {
        console.log(error);
      }
    },
    capitalize(string) {
      console.log(string)
      return string.charAt(0).toUpperCase() + string.slice(1)
    }
  },
  created() {
    this.getData();
  },
};
</script>

<style scoped lang="scss">
  #finder{
    text-align: center;
    width: 70vw;
    margin-left: auto;
    margin-right: auto;
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    color: rgb(46, 89, 168);
  }
  ul{
    list-style: none;
    margin-block-start: 0;
    padding-inline-start: 0;
    font-weight: lighter;
    font-size: small;
    line-height: 1rem;
    color: steelblue;
  }
  #pokemonlogo{
    width: 400px;
  }
  button{
    border: 1px solid rgb(235, 190, 45);
    background: none;
    padding-top: 2px;
    padding-bottom: 2px;
    color: rgb(55, 60, 66);
  }
  input{
    border: 1px solid rgb(235, 190, 45);
    padding-top: 2px;
    padding-bottom: 2px;
    color: rgb(67, 74, 82);
  }
</style>