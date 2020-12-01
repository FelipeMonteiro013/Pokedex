<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <h1 class="is-size-1">Pokedéx</h1>
      <hr />
      <div id="teste">
        <input
          class="input"
          type="text"
          placeholder="Pesquisar pelo nome"
          v-model="busca"
        />
        <button id="pesquisar" class="button is-success" @click="buscar">Pesquisar</button>
        <button id="pesquisar" class="button is-info" @click="buscar">Limpar</button>
      </div>

      <div v-for="(poke) in filteredPokemons" :key="poke.url">
        <!-- Passando por parametro os dados que vem da API para o componente Pokemon -->
        <Pokemon :name="poke.name" :url="poke.url"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon.vue";
export default {
  name: "App",
  components: {
    Pokemon,
  },
  methods:{
    buscar: function(){
      this.filteredPokemons = this.pokemons;
      if (this.busca == '' || this.busca == ' ') {
        this.filteredPokemons = this.pokemons
        console.log(this.pokemons);
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name.indexOf(this.busca) > -1)
        console.log(this.filteredPokemons);
      }
    }
  },
  computed:{
    // resultadoBusca: function () {
    //   if (this.busca == '' || this.busca == ' ') {
    //     return this.pokemons        
    //   }else{
    //     return this.pokemons.filter(pokemon => pokemon.name == this.busca);
    //   }
    // }
  },
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: "",
    };
  },
  //Função chamada assim que a pagina carrega
  created: function () {
    // Requisição HTTP utilizando o axios
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.results;
      });
  },
};
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

#teste {
  display: flex;
  justify-content: space-around;
}

#pesquisar{
  margin-left: 1%;
}
</style>
