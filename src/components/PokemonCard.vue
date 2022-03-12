<template>
  <div class="card mb-3">
    <div class="row g-0">
      <div class="d-flex flex-wrap col-4">
        <img :src="currentImg" class="img-fluid rounded-start" alt="">
      </div>
      <div class="d-flex flex-wrap col-8" id="">
        <div class="card-body" id="">
          <h5 class="card-title"> <p class="capitalized">{{ name }}</p></h5>
          <div >
            <pokemon-card-detail 
              :type="pokemon.type"
              :height="pokemon.height"
              :weight="pokemon.weight"
            />
          </div>
        </div>
        
      </div> 
  </div>  
</div>

</template>
<script>
import api from '../services/api';
import PokemonCardDetail from './PokemonCardDetail.vue'
export default {
  name: 'PokemonCard',
  components:{
    PokemonCardDetail
  },
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

<style scoped>
  .capitalized {
	text-transform: capitalize;
}
</style>
