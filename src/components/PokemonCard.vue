<template>
  <div class="card mb-3" style="max-width: 400px;">
  <div class="row g-0">
    <div class="col-md-4">
      <img style="margin-top: 50px;" :src="currentImg" class="img-fluid rounded-start" alt="">
    </div>
    <div class="col-md-8">
      <div class="card-body">
        <h5 class="card-title"> {{ name}}</h5>
          <p class="subtitle is-6">Tipo: {{ pokemon.type }}</p>
          <p class="subtitle is-6">Altura: {{ pokemon.height / 10 }} m</p>
          <p class="subtitle is-6">Peso: {{ pokemon.weight / 10 }} kg</p>
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
    index: Number,
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
      pokemon: {
        type:'',
        height:'',
        weight: ''
      }
    }
  },
}
</script>
