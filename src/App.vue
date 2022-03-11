<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <div class="container-fluid">
    <a class="navbar-brand" href=""><span  class="img-logo img-responsive" alt="Responsive image"></span></a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <li class="nav-item">
          <a class="nav-link active"><span  @click="highContrast()">teste</span></a>
        </li>
      </ul>
      <form @submit.prevent="searchPokemons" class="d-flex">
        <input class="form-control me-2" type="search" aria-label="Search" v-model="search">
        <button class="btn btn-outline-success" type="submit" >Pesquisar</button>
      </form>
    </div>
  </div>
</nav>

  <div class="container">
    <div class="row">
      <div class="col-12 col-md-3" v-for="(pokemon, index) in filteredPokemons" :key="pokemon.url" >
        <pokemon-card :index="index + 1" :name="pokemon.name" :url="pokemon.url" />
      </div>
  </div>
  </div>
  
</template>

<style scoped>
.img-logo {
  height: 60px;
  width: 200px;
  display: block;
  background: url('assets/logoPokemon.png') no-repeat;
  background-size: contain;
  color: transparent;
}
.high-contrast {
  background: black !important;
  color: white !important;
  border-color: white !important; }
  .high-contrast nav {
    background: black !important;
    color: white !important;
    border-color: white !important; }
  .high-contrast div {
    background: black !important;
    color: white !important;
    border-color: white !important;
    border-bottom: 1px solid white; }
  .high-contrast nav {
    border-bottom: 1px solid white; }
  .high-contrast body, .high-contrast h1, .high-contrast h2, .high-contrast h3, .high-contrast h4, .high-contrast h5, .high-contrast p, .high-contrast .contrast span {
    color: white !important; }
  .high-contrast option, .high-contrast body {
    background: black !important;
    color: yellow !important; }
  .high-contrast td {
    background: black !important;
    color: white !important; }
  .high-contrast img {
    background: white !important;
    color: yellow !important; }
  .high-contrast ul, .high-contrast li {
    background: black !important;
    color: yellow !important; }
  .high-contrast a, .high-contrast button {
    background: black !important;
    color: yellow !important;
    border: 1px solid yellow !important; }
  .high-contrast select, .high-contrast input {
    background: black !important;
    color: white !important;
    border: 1px solid white !important; }
</style>

<script>
import api from './services/api';
import PokemonCard from './components/PokemonCard.vue';
export default {
  name: 'App',
  components: {
    PokemonCard
  },
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      search: ''
    }
  },
  created: function() {
    api.get('pokemon?limit=269&offset=0').then((response) => { 
      this.pokemons = response.data.results;
      this.filteredPokemons = response.data.results;
    });
  },
  methods: {
    searchPokemons: function() {
      this.filteredPokemons = this.pokemons;
      if(this.search == '' || this.search == '  ') {
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter((pokemon) => pokemon.name == this.search);
      }
    }
  },
  highContrast(){
    if(!this.contrast){
      document.body.classList.add('high-contrast');
    }else{
      document.body.classList.remove('high-contrast');
    }
    this.contrast = !this.contrast;
  }
}
</script>

