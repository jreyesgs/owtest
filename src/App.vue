<template>
  <main class="container">
    <div class="row">
      <div>
        <h1>The Rick and Morty Caracters</h1>
      </div>
    </div>
    <nav class="justify-content-center">
      <ul class="nav">
        <li class="nav-item">
          <a class="nav-link item" @click="showCharacter">Characters</a>
        </li>
        
        <li class="nav-item ">
          <a class="nav-link item" @click="showEpisodes">Episodes</a>
        </li>
      </ul>
      <!-- TODO: Crea algún sistema para navegar de un componente a otro -->
    </nav>
    <Characters v-if="isVisibleComponent" />
    <Episodes v-if="isVisibleEpisodes" />
  </main>
</template>

<script>
import Characters from "./components/Characters.vue";
import Episodes from "./components/Episodes.vue";
export default {
  name: "App",
  components: {
    Characters,
    Episodes,
  },
  data() {
    return {
      isVisibleComponent: true,
      isVisibleEpisodes: false,
    };
  },
  methods: {
    showCharacter() {
      this.isVisibleComponent = true;
      this.isVisibleEpisodes = false;
    },
    showEpisodes() {
      this.isVisibleEpisodes = true;
      this.isVisibleComponent = false;
    },
  },
};
</script>

<style lang="scss">
:root {
  --background-body: #24282f;
  --background-card: #3c3e44;
  --text-white: #fff;
  --text-gray: #c0c0c0;
  --text-orange: #ff9800;
}
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  background-color: var(--background-body) !important;
  color: var(--text-white) !important;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif !important;
}
h5 {
  margin-bottom: 3rem !important;
  text-align: center !important;
}

img {
  width: 100% !important;
}
.item {
  padding: 1rem 0.5rem;
  color: var(--text-white) !important;
  background-color: var(--background-card);
  text-align: center;
  cursor: pointer !important;
  &:hover {
    color: var(--text-orange) !important;
  }
}
</style>
