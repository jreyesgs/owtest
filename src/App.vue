<template>
<main class="container">
  <div class="row">
    <dvi class="col">
      <h1>The Rick and Morty Caracters</h1>
    </dvi>
  </div>
  <Character />
</main>
</template>

<script>
import Character from "./components/Character.vue"

export default {
  name: 'App',
  components: {
    Character
  }
}
    // https://rickandmortyapi.com/api/character
</script>

<style lang="scss">

</style>
