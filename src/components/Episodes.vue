<template>
 <div class="row mt-3">
  <div v-for="episode in episodes" :key="episode.id" class="col-lg-4">
      <div class="card" style="width: 18rem;">
  <div class="card-header">
    {{episode.name}}
  </div>
  <div>
    {{episode.air_date}}
  </div>
  
  <div>
    <button class="btn btn-primary" @click="getCharacter(episode.id)" data-bs-toggle="modal" data-bs-target="#staticBackdrop">View Characters</button>
  </div>

 
</div>
  </div>
 </div>
 
<div class="modal fade" id="staticBackdrop" data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1" aria-labelledby="staticBackdropLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="staticBackdropLabel">List Characters</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        <div class="row mt-3 justify-content-center">
        <div v-for="characterInfo in charactersInfo" :key="characterInfo.id" class="col-lg-4">
  
      <span>{{characterInfo.name}}</span>
       <span><img :src="characterInfo.image" alt="" srcset=""></span>
   
      </div>
    </div>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
      </div>
    </div>
  </div>
</div>
</template>

<script>
import axios from 'axios'
export default {
  data(){
    return{
      urlApi:'https://rickandmortyapi.com/api/episode',
      episodes:[],
      characters:[],
      isListVisible: false,
      charactersInfo:[]
     
    }
    
  },
  created(){
this.getEpisodes()

  },
methods:{
  getEpisodes(){
    axios.get(this.urlApi)
    .then((res)=>{
     
            this.episodes = res.data.results
            this.characters = res.data.results.characters
            
    })
    .catch((error)=>{
      console.log(error)
    })

  },
  getCharacter(id){
            this.charactersInfo = []
            axios.get(this.urlApi+'/'+id)
            .then((res)=>{
              
                res.data.characters
                
              for(let i = 0; i < res.data.characters.length; i++){
                axios.get(res.data.characters[i])
                .then((res)=>{
                  console.log(res.data)
                 this.charactersInfo.push(res.data)
                 
                })
                .catch((error)=>{
                  console.log(error)
                })
              }
            })
            .catch((error)=>{
              console.log(error)
            })
           
       
      }
       
  
}
}
</script>

<style scoped>
span, h5{
  color: black !important;
}
</style>