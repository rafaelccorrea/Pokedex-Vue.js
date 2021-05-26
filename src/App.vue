<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/logo.png">
      <hr>
      <h4 class="is-size-4">Pokedex</h4>
      <input class="input is-primary" type="text" placeholder="Buscar Pokemon: " v-model="busca">
      <button @click="buscar" id="BtnBusca" class="button is-primary is-focused">Buscar</button>
        <div v-for="(poke) in filterPokemons" :key="poke.url">
            <Pokemon :name="poke.name" :url="poke.url" :number="poke.index+1"/>
        </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon"

export default {
  name: 'App',
  data(){
    return {
      pokemons: [],
      filterPokemons: [],
      busca: ''
    }
  },
  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then((res) =>{
      this.pokemons = res.data.results;
      this.filterPokemons = res.data.results;
    });
  },
  components:{
    Pokemon
  },
  methods:{
    buscar: function(){
      this.filterPokemons = this.pokemons;
      if(this.busca == '' || this.busca == ' '){
          this.filterPokemons = this.pokemons;
      }else{
        this.filterPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
  },
  /*computed: {
    resultsbusca: function(){
      if(this.busca == '' || this.busca == ' '){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
  } */
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#BtnBusca{
  margin-top: 2%;
}
</style>
