<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
        <img src="./assets/logo1.png" id="logo" class="mb-6">

        <input class="is-rounded input mb-5" type="text" placeholder="Pesquisar pokemon. Exemplo: bulbasaur" v-model="busca">
        <button @click="buscar()" class="button is-warning is-small is-fullwidth mb-6">Search</button>

        <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :num="index + 1" :name="poke.name" :url="poke.url" />
        </div>
    </div>
  </div>
</template>

<script>

  import axios from 'axios'
  import Pokemon from './components/Pokemon'

  export default {
    name: 'App',

    data () {
      return {
        pokemons: [],
        filteredPokemons: [],
        busca: ''
      }
    },

    created () {
      axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
        
        this.pokemons = res.data.results // Lista de pokemons
        this.filteredPokemons = res.data.results // Filtro de pokemons
        
      }).catch(error => {console.log(error)})
    },

    components: {
      Pokemon
    },

    methods: {
      buscar () {
        this.filteredPokemons = this.pokemons
        if (this.busca == '' | this.busca == ' ') {
        this.filteredPokemons = this.pokemons

        } else {
          this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca)

        }
      }
    }
  }

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #4e8d6b;
  height: 100%;
}

#logo {
  width: 300px;
}
</style>
