<template>
  <div class="card" data-bs-toggle="modal" data-bs-target="#card" >
        <div class="row g-0">
          <div class="col-md-4">
            <img
              :src="character.image"
              class="img-fluid rounded-start"
              alt=""
            />
          </div>
          <div class="col-md-8">
            <div class="card-body">
              <h5 class="card-title">{{ character.name }}</h5>
              <div class="status">
                <span
                  :class="
                    character.status == 'Alive'
                      ? 'alive'
                      : character.status == 'Dead'
                      ? 'dead'
                      : 'default'
                  "
                ></span>
                <span
                  >{{ character.status }} - {{ character.species }} -
                  {{ character.gender }}</span
                >
              </div>

              <p class="card-text">
                <small class="text-muted">{{ character.origin.name }}</small>
              </p>

              <!-- TODO: Añade un botón que abra el detalle del personaje a través de un modal-->
            </div>
          </div>
        </div>
      </div>
</template>

<script>
export default {
props:['character']
}
</script>

<style>

</style>