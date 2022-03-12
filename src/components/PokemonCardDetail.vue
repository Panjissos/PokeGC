<template>
    <div class="modal fade" id="exampleModalToggle" aria-hidden="true" aria-labelledby="exampleModalToggleLabel" tabindex="-1">
          <div class="modal-dialog modal-dialog-centered">
              <div class="modal-content">
              <div class="modal-header">
                  <h5 class="modal-title" id="exampleModalToggleLabel">Detalhes</h5>
                  <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
              </div>
              <div class="modal-body">
                  <div style="margin-right: 50px;">
                    <p class="subtitle is-6">Tipo: {{ type }}</p>
                    <p class="subtitle is-6">Altura: {{ height / 10 }} M</p>
                    <p class="subtitle is-6">Peso: {{ weight / 10 }} Kg</p>
                  </div>
              </div>
              <div class="modal-footer">
                  <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Fechar</button>
              </div>
              </div>
          </div>
      </div>
      <a class="btn btn-dark" data-bs-toggle="modal" href="#exampleModalToggle" role="button">detalhes</a>  
</template>
<script>

export default {
    props: [
       'type',
       'height',
       'weight'
    ]
}
</script>