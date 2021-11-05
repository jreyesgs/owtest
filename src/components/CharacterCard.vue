<template>
  <div class="card" data-bs-toggle="modal" data-bs-target="#card">
    <div class="row g-0">
      <div class="col-md-4">
        <img :src="character.image" class="img-fluid rounded-start" alt="" />
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

          <span class="text-muted">{{ character.origin.name }}</span>

          <!-- TODO: Añade un botón que abra el detalle del personaje a través de un modal-->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["character"],
};
</script>

<style lang="scss">
.card {
  background-color: var(--background-card) !important;
  border-radius: 20px;
  box-shadow: 0 0 10px 1px var(--background-body);
  overflow: hidden;
  cursor: pointer;
  transition: transform 200ms ease-in-out;
  height: 100%;
  &:hover {
    transform: scale(1.05);
    h5 {
      color: var(--text-orange);
    }
  }
  span {
    color: var(--text-gray) !important;
  }

  h5 {
    margin-bottom: 0.5rem !important;
  }
}
.img-fluid{
        width: 100%!important;
    height: 100%!important;
    margin: 0px!important;
    opacity: 1!important;
    transition: opacity 0.5s ease 0s;
    object-position: center center!important;
    object-fit: cover!important;

}
</style>