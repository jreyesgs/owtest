<template>
 <div class="row mt-3">
  <div v-for="episode in episodes" :key="episode.id" class="col-lg-4">
      <!-- 
          TODO: Crea el listado de episodios con cards y añadir el detalle del episodios con la vista previa de los personajes.
      -->
      <div class="card" style="width: 18rem;">
  <div class="card-header">
    {{episode.name}}
  </div>
  <div>
    {{episode.air_date}}
  </div>
  <!-- <div>
    <button @click="getCharacter()">View Characters</button>
  </div>
  <ul class="list-group list-group-flush" v-for="character in characters" :key="character.id" >
    <li class="list-group-item"><img :src="character.image" alt="">
    <span>{{characters.name}}</span></li>
   
  </ul> -->
</div>
  </div>
 </div>
</template>

<script>
import axios from 'axios'
export default {
  data(){
    return{
      episodes:[],
      characters:[]
    }
    
  },
  created(){
this.getEpisodes()

  },
methods:{
  getEpisodes(){
    axios.get('https://rickandmortyapi.com/api/episode')
    .then((res)=>{
       for (let i = 0; i < res.data.results.length; i++) {
            this.episodes.push(res.data.results[i]);
       }
     console.log(this.episodes)
    })
    .catch((error)=>{
      console.log(error)
    })

  },
  // getCharacter(){
  //   for(let i = 0; i < this.episodes.length; i++){
  //     console.log(this.episodes[i].characters)
  //     for(let j= 0; j < this.episodes[i].characters.length; j++){
  //           axios.get(''+this.episodes[i].characters[j]+'')
  //           .then((res)=>{
  //             console.log(res.data)
  //             this.characters.push(res.data)
  //             console.log(this.characters)
  //           })
  //           .catch((error)=>{
  //             console.log(error)
  //           })
  //         }

  //     }
       
  // }
}
}
</script>

<style>

</style>