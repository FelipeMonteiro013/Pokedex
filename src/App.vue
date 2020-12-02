<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <h1 class="is-size-1">Pokedéx</h1>
      <hr />
      <div id="teste">
        <button id="pesquisar" class="button is-info" @click="geracao(1)">
          Gereção 1
        </button>
        <button id="pesquisar" class="button is-info" @click="geracao(2)">
          Gereção 2
        </button>
        <button id="pesquisar" class="button is-info" @click="geracao(3)">
          Gereção 3
        </button>
        <button id="pesquisar" class="button is-info" @click="geracao(4)">
          Gereção 4
        </button>
        <button id="pesquisar" class="button is-info" @click="geracao(5)">
          Gereção 5
        </button>
        <button id="pesquisar" class="button is-info" @click="geracao(6)">
          Gereção 6
        </button>
        <button id="pesquisar" class="button is-info" @click="geracao(7)">
          Gereção 7
        </button>
        <button id="pesquisar" class="button is-info" @click="geracao(8)">
          Gereção 8
        </button>
      </div>
      <div id="teste">
        <input
          class="input"
          type="text"
          placeholder="Pesquisar pelo nome"
          v-model="busca"
        />
        <button id="pesquisar" class="button is-success" @click="buscar">
          Pesquisar
        </button>
        <button id="pesquisar" class="button is-info" @click="limpar">
          Limpar
        </button>
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
  methods: {
    buscar: function () {
      this.filteredPokemons = this.pokemons;
      if (this.busca == "" || this.busca == " ") {
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter(
          (pokemon) => pokemon.name.indexOf(this.busca) > -1
        );
      }
    },
    limpar: function(){
      this.busca = ""
      this.filteredPokemons =  this.pokemons
    },
    geracao: function (value) {
      if (value == 2) {
        axios
          .get("https://pokeapi.co/api/v2/pokemon?limit=100&offset=151")
          .then((res) => {
            this.pokemons = res.data.results;
            this.filteredPokemons = res.data.results;
          });
      } else if (value == 3) {
        axios
          .get("https://pokeapi.co/api/v2/pokemon?limit=135&offset=251")
          .then((res) => {
            this.pokemons = res.data.results;
            this.filteredPokemons = res.data.results;
          });
      } else if (value == 4) {
        axios
          .get("https://pokeapi.co/api/v2/pokemon?limit=107&offset=386")
          .then((res) => {
            this.pokemons = res.data.results;
            this.filteredPokemons = res.data.results;
          });
      } else if (value == 5) {
        axios
          .get("https://pokeapi.co/api/v2/pokemon?limit=156&offset=493")
          .then((res) => {
            this.pokemons = res.data.results;
            this.filteredPokemons = res.data.results;
          });
      } else if (value == 6) {
        axios
          .get("https://pokeapi.co/api/v2/pokemon?limit=72&offset=649")
          .then((res) => {
            this.pokemons = res.data.results;
            this.filteredPokemons = res.data.results;
          });
      } else if (value == 7) {
        axios
          .get("https://pokeapi.co/api/v2/pokemon?limit=88&offset=721")
          .then((res) => {
            this.pokemons = res.data.results;
            this.filteredPokemons = res.data.results;
          });
      } else if (value == 8) {
        axios
          .get("https://pokeapi.co/api/v2/pokemon?limit=89&offset=809")
          .then((res) => {
            this.pokemons = res.data.results;
            this.filteredPokemons = res.data.results;
          });
      }else{
        axios
          .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
          .then((res) => {
            this.pokemons = res.data.results;
            this.filteredPokemons = res.data.results;
          });
      }
    },
  },
  computed: {
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
  margin-top: 1%;
}

#pesquisar {
  margin-left: 1%;
}
</style>
