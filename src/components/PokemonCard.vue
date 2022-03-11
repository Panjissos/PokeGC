<template>
  <div class="card mb-3">
    <div class="row g-0">
      <div class="d-flex flex-wrap col-4">
        <img :src="currentImg" class="img-fluid rounded-start" alt="">
      </div>
      <div class="d-flex flex-wrap col-8">
        <div class="card-body">
          <h5 class="card-title"> <p class="capitalized">{{ name}}</p></h5>
            <div class="modal fade" id="exampleModalToggle" aria-hidden="true" aria-labelledby="exampleModalToggleLabel" tabindex="-1">
          <div class="modal-dialog modal-dialog-centered">
              <div class="modal-content">
              <div class="modal-header">
                  <h5 class="modal-title" id="exampleModalToggleLabel">Modal 1</h5>
                  <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
              </div>
              <div class="modal-body">
                  <p class="subtitle is-6">Tipo: {{ pokemon.type }}</p>
                  <p class="subtitle is-6">Altura: {{ pokemon.height / 10 }} M</p>
                  <p class="subtitle is-6">Peso: {{ pokemon.weight / 10 }} Kg</p>
              </div>
              <div class="modal-footer">
                  <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
              </div>
              </div>
          </div>
      </div>
      <a class="btn btn-dark" data-bs-toggle="modal" href="#exampleModalToggle" role="button">detalhes</a>
        </div>
      </div> 
  </div>
  
</div>

</template>
<script>
import api from '../services/api';
//import PokemonDetails from './PokemonDetails.vue';
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
      pokemon: {
        type:'',
        height:'',
        weight: ''
      }
    }
  },
}
</script>
<style scoped>
  .capitalized {
	text-transform: capitalize;
}
</style>
