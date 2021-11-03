<template>
<main class="container">
  <div class="row">
    <dvi class="col mt-3">
      <h1>The Rick and Morty Caracters</h1>
    </dvi>
  </div>
  <nav>
    <!-- TODO: Crea algún sistema para navegar de un componente a otro -->
  </nav>
  <Characters />
</main>
</template>

<script>
import Characters from "./components/Characters.vue"

export default {
  name: 'App',
  components: {
    Characters
  }
}

</script>

<style lang="scss">
  // TODO: Añade los estilos que consideres necesarios.
</style>
