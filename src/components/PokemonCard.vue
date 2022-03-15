<template>
  <div class="card mb-3">
    <div class="row g-0">
      <div class="d-flex flex-wrap col-4">
        <img :src="currentImg" class="img-fluid img-thumbnail" alt="">
      </div>
      <div class="d-flex flex-wrap col-8" id="">
        <div class="card-body" id="">
          <h5 class="card-title"> <p class="capitalized">{{ name }}</p></h5>
          <div >
            <p class="subtitle is-6">Tipo: {{ pokemon.type }}</p>
            <p class="subtitle is-6">Altura: {{ pokemon.height / 10 }} M</p>
            <p class="subtitle is-6">Peso: {{ pokemon.weight / 10 }} Kg</p>
          </div>
        </div>
      </div> 
  </div>  
</div>
</template>
<script>
import api from '../services/api';
export default {
  name: 'PokemonCard',
  props: {
    name: String,
    url: String
  },
  created: function() {
    api.get(this.url).then((response) => {
      this.pokemon.type = response.data.types[0].type.name;
      this.currentImg = response.data.sprites.front_default;
      this.pokemon.height = response.data.height;
      this.pokemon.weight = response.data.weight;
    });
  },
  data(){
    return {
      currentImg: '',
      pokemon: {}
    }
  },
}
</script>

<style scoped>
  .capitalized {
	text-transform: capitalize;
}
</style>
