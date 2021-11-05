<template>
  <div class="row">
    <div class="col">
      <h2>List of Character</h2>
    </div>
  </div>
  <!-- Utiliza componentes siempre que sea necesarios para mejorar la usabilidad del código -->
  <nav class="navbar navbar-expand-lg">
 <div class="container-fluid">
    <a class="navbar-brand item" @click.prevent="filterStatus('')">All</a>
    
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
       
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
            Status
          </a>
          <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
            <li><a class="dropdown-item item" @click.prevent="filterStatus('Alive')" >Alive</a></li>
            <li><hr class="dropdown-divider"></li>
            <li><a class="dropdown-item item" @click.prevent="filterStatus('Dead')">Dead</a></li>
            <li><hr class="dropdown-divider"></li>
            <li><a class="dropdown-item item" @click.prevent="filterStatus('unknown')">Unknown</a></li>
          </ul>
        </li>
       <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
            Species
          </a>
          <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
            <li><a class="dropdown-item item" @click.prevent="filterSpecies('Human')">Human</a></li>
            <li><hr class="dropdown-divider"></li>
            <li><a class="dropdown-item item" @click.prevent="filterSpecies('Alien')">Alien</a></li>
           
          </ul>
        </li>
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
            Gender
          </a>
          <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
            <li><a class="dropdown-item item" @click="filterGender('Male')">Male</a></li>
            <li><hr class="dropdown-divider item"></li>
            <li><a class="dropdown-item item" @click="filterGender('Female')">Female</a></li>
            <li><hr class="dropdown-divider"></li>
            <li><a class="dropdown-item item" @click="filterGender('Genderless')">Genderless</a></li>
            <li><hr class="dropdown-divider"></li>
            <li><a class="dropdown-item item" @click="filterGender('Unknown')">Unknown</a></li>
          </ul>
        </li>
      </ul>
      <form class="d-flex">
        <input class="form-control me-2" v-model="name" type="search" placeholder="Search by name" aria-label="Search">
        <button class="btn btn-outline-success" @click.prevent="getCharacter()" type="submit">Search</button>
      </form>
    </div>
  </div>
  </nav>
  <div class="row mt-3">
    <div v-for="character in characters" :key="character.id" class="col-lg-4">
      <!--
            TODO: Añadir los datos de las fichas de los personajes para completarla:

            - Nombre
            - Estado
            - Especie
            - Genero
            - Origen
            ...Resto de datos

            Para que quede una card al estilo: https://rickandmortyapi.com/

            Usando como base esta card de Bootstrap 5, modificala para adaptarla a las necesidades de los datos.

        -->
      <div class="card mb-3" data-bs-toggle="modal" data-bs-target="#card"  @click="showModal(character)">
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
              <p class="card-text">
                {{ character.status }} - {{ character.species }} -
                {{ character.gender }}
              </p>
              <p class="card-text">
                <small class="text-muted">{{ character.origin.name }}</small>
              </p>
            
              <!-- TODO: Añade un botón que abra el detalle del personaje a través de un modal-->
               
            </div>
          </div>
        </div>
      </div>
          
    </div>
  
  </div>
  
  <div class="modal fade" id="card" tabindex="-1" aria-labelledby="cardInfo" >
  <div class="modal-dialog">
   
     
<div class="modal-body"> 
<CaracterDetail v-if="isModalVisible"  :character='characterInfo'/> 
    

</div>
</div>
</div>
  <footer>
   	<!-- <nav class="app-pagination">
							<ul class="pagination justify-content-center">
								<li class="page-item ">
									<a class="page-link" href="#" v-if="pages.current > 1" @click.prevent="changePage(pages.current - 1)">Anterior</a>
							    </li>
								
								<li class="page-item " exact-active-class="active" v-for="page in pagesNumber" :key="page.to"  @click.prevent="changePage(page)"><a class="page-link" href="#"  >{{page}}</a></li>
								
								<li class="page-item">
								    <a class="page-link" href="#" v-if="pages.current <  pages.last_page" @click.prevent="changePage(pages.current + 1)">Siguiente</a>
								</li>
							</ul>
						</nav>//app-pagination -->
  </footer>

</template>

<script>
import axios from "axios";
import CaracterDetail from '@/components/CaracterDetail.vue'
export default {
  name: "Character",
  components: {CaracterDetail},
  data() {
    return {
      characters: [],
      name: "",
      pages:'',
      isModalVisible: false,
      characterInfo:{}
    };
  },
  created(){
     this.getCharacters()



  },

  methods: {
    getCharacters(){
         axios.get('https://rickandmortyapi.com/api/character') 
         .then((res)=>{
             for (let i = 0; i < res.data.results.length; i++) {
            this.characters.push(res.data.results[i]);
          }
         })
         .catch((error)=>{
           console.log(error)
         })
      },
    getCharacter() {
      this.characters = [];
      const formatName = this.name.toLowerCase();
      axios
        .get("https://rickandmortyapi.com/api/character/?name=" + formatName)
        .then((res) => {
          for (let i = 0; i < res.data.results.length; i++) {
            this.characters.push(res.data.results[i]);
          }
        })
         .catch((error)=>{
           console.log(error)
         });
    },
    filterStatus(status) {
      this.characters = [];
      const formatName = this.name.toLowerCase();
      axios
        .get(
          "https://rickandmortyapi.com/api/character/?name=" +
            formatName +
            "&status=" +
            status
        )
        .then((res) => {
          
          for (let i = 0; i < res.data.results.length; i++) {
            this.characters.push(res.data.results[i]);
          }
        })
         .catch((error)=>{
           console.log(error)
         });
    },
    filterSpecies(specie) {
      this.characters = [];
      const formatName = this.name.toLowerCase();
      axios
        .get(
          "https://rickandmortyapi.com/api/character/?name=" +
            formatName +
            "&species=" +
            specie
        )
        .then((res) => {
          
          for (let i = 0; i < res.data.results.length; i++) {
            this.characters.push(res.data.results[i]);
          }
        })
         .catch((error)=>{
           console.log(error)
         });
    },
    filterGender(gender) {
      this.characters = [];
      const formatName = this.name.toLowerCase();
      axios
        .get(
          "https://rickandmortyapi.com/api/character/?name=" +
            formatName +
            "&gender=" +
            gender
        )
        .then((res) => {
         
          for (let i = 0; i < res.data.results.length; i++) {
            this.characters.push(res.data.results[i]);
          }
        })
         .catch((error)=>{
           console.log(error)
         });
    },
    showModal(data) {
      this.characterInfo = data;
       this.isModalVisible = !this.isModalVisible;
       
      
      
      console.log(this.characterInfo)
    },
  },
};
</script>

<style lang="scss">
button{
    border: 2px solid white!important;
    color: var(--text-white)!important
}
.mt-3{
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 3rem;
    margin: 3rem 0;
}
.card{
  background-color: var(--background-card)!important;
  border-radius: 20px;
  box-shadow: 0 0 10px 1px var(--background-body);
  overflow: hidden;
  cursor: pointer;
  transition: transform 200ms ease-in-out;
  height: 100%;
  &:hover{
    transform: scale(1.05);
    h5{
      color: var(--text-orange);
    }
  }
  span{
    color: var(--text-gray)!important;
  }
  h5{
    margin-bottom: 0.5rem!important;
  }
 
    .origen{
      margin-bottom: 0.5rem;
    }


}
  .search{
    width: 400px;
    margin: 3rem auto 0;
    input{
        height: 53px;
        width: 400px;
        border: none;
        border-radius: 10px;
        padding: 0 0.5rem;
    }
}
.filter{
    width: 400px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    border-radius: 10px;
    overflow: hidden;
    .item{
        padding: 1rem 0.5rem;
        background-color: var(--background-card);
        text-align: center;
        cursor: pointer;
        &:hover{
            color: var(--text-orange);
        }
        
    }
}
</style>