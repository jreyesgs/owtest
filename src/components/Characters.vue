<template>
  <div class="row">
    <div class="col">
      <h2>List of Character</h2>
    </div>
  </div>
  <!-- Utiliza componentes siempre que sea necesarios para mejorar la usabilidad del código -->
  <div class="d-flex justify-content-between">
    <ul class="nav nav-tabs">
      <li class="nav-item">
        <a
          class="nav-link item"
          aria-current="page"
          href="#"
          @click.prevent="getCharacters()"
          >All</a
        >
      </li>
      <li class="nav-item dropdown">
        <a
          class="nav-link item dropdown-toggle"
          data-bs-toggle="dropdown"
          href="#"
          role="button"
          aria-expanded="false"
          >Status</a
        >
        <ul class="dropdown-menu">
          <li>
            <a class="dropdown-item" @click.prevent="filterBy('status','Alive')"
              >Alive</a
            >
          </li>
          <li><hr class="dropdown-divider" /></li>
          <li>
            <a class="dropdown-item" @click.prevent="filterBy('status','Dead')"
              >Dead</a
            >
          </li>
          <li><hr class="dropdown-divider" /></li>
          <li>
            <a class="dropdown-item" @click.prevent="filterBy('status','unknown')"
              >Unknown</a
            >
          </li>
        </ul>
      </li>
      <li class="nav-item dropdown">
        <a
          class="nav-link item dropdown-toggle"
          data-bs-toggle="dropdown"
          href="#"
          role="button"
          aria-expanded="false"
          >Gender</a
        >
        <ul class="dropdown-menu">
          <li>
            <a class="dropdown-item" @click.prevent="filterBy('gender','Male')">Male</a>
          </li>
          <li><hr class="dropdown-divider" /></li>
          <li>
            <a class="dropdown-item" @click.prevent="filterBy('gender','Female')">Female</a>
          </li>
          <li><hr class="dropdown-divider" /></li>
          <li>
            <a class="dropdown-item" @click.prevent="filterBy('gender','Genderless')"
              >Genderless</a
            >
          </li>
          <li><hr class="dropdown-divider" /></li>
          <li>
            <a class="dropdown-item" @click.prevent="filterBy('gender','Unknown')"
              >Unknown</a
            >
          </li>
        </ul>
      </li>
      <li class="nav-item dropdown">
        <a
          class="nav-link item dropdown-toggle"
          data-bs-toggle="dropdown"
          href="#"
          role="button"
          aria-expanded="false"
          >Species</a
        >
        <ul class="dropdown-menu">
          <li>
            <a class="dropdown-item" @click.prevent="filterBy('species','Human')"
              >Human</a
            >
          </li>
          <li><hr class="dropdown-divider" /></li>
          <li>
            <a class="dropdown-item" @click.prevent="filterBy('species','Alien')"
              >Alien</a
            >
          </li>
        </ul>
      </li>
    </ul>
    <form class="d-flex">
      <input
        class="form-control me-2"
        v-model="name"
        type="search"
        placeholder="Search by name"
        aria-label="Search"
      />
      <button
        class="btn btn-outline-success"
        @click.prevent="searchByName(name)"
        type="submit"
      >
        Search
      </button>
    </form>
  </div>
  <div class="row mt-3 justify-content-center">
    <div v-for="character in characters" :key="character.id" class="col-lg-4">
      <CharacterCard @click="passCharacter(character)" :character="character" />
    </div>

    <CaracterDetail :character="characterInfo" />
  </div>

  <!-- <CaracterDetail  :character="characterInfo" /> -->
</template>

<script>
import axios from "axios";
import CaracterDetail from "@/components/CaracterDetail.vue";
import CharacterCard from "@/components/CharacterCard.vue";
export default {
  name: "Character",
  components: { CaracterDetail, CharacterCard },
  data() {
    return {
      characters: [],
      name: "",
      isModalVisible: false,
      characterInfo: null,
      apiUrl: "https://rickandmortyapi.com/api/character",
    };
  },
  created() {
    this.getCharacters();
  },

  methods: {
    getCharacters() {
      axios
        .get(this.apiUrl)
        .then((res) => {
          this.characters = res.data.results;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    searchByName(name) {
      axios
        .get(this.apiUrl + "/?name=" + name.toLowerCase())
        .then((res) => {
          this.characters = res.data.results;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    filterBy(param,value){
     if(this.name == ''){
 axios
        .get(this.apiUrl + "/?" + param +'='+ value)
        .then((res) => {
          this.characters = res.data.results;
        })
        .catch((error) => {
          console.log(error);
        });
     }
     else{
        axios
        .get(this.apiUrl + "/?name="+this.name + '&'+ param +'='+ value)
        .then((res) => {
          this.characters = res.data.results;
        })
        .catch((error) => {
          console.log(error);
        });
     }
      
    },
    passCharacter(character) {
      this.characterInfo = character;
    },
  },
};
</script>

<style lang="scss">
button {
  border: 2px solid white !important;
  color: var(--text-white) !important;
}
.mt-3 {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 3rem;
  margin: 3rem 0;
}

.search {
  width: 400px;
  margin: 3rem auto 0;
  input {
    height: 53px;
    width: 400px;
    border: none;
    border-radius: 10px;
    padding: 0 0.5rem;
  }
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
.card-body {
  padding: 0rem 1rem !important;
}

.status {
  display: flex;
  align-items: center;
  margin-bottom: 0.5rem;
  span {
    color: var(--text-gray);
    &:first-child {
      width: 10px;
      height: 10px;
      border-radius: 50%;
      margin-right: 0.5rem;
    }
  }
  .alive {
    background-color: green;
  }
  .dead {
    background-color: red;
  }
  .default {
    background-color: white;
  }
}
</style>