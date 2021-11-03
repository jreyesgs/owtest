<template>
<div class="row">
    <div class="col">
        <h2>List of Character</h2>
    </div>
</div>
<nav>
    <!-- 
            TODO: Añadir aquí una barra de navegación que permita realizar filtros sobre los resultados por:
            
            name: filtrar por el dado name.
            status: filtrar por el dado status (alive, dead or unknown).
            species: filtrar por el dado species (Human, Alien).
            gender: filtrar por el dado gender (female, male, genderless or unknown).

            https://rickandmortyapi.com/documentation/#rest
    -->
</nav>
<div class="row">
    <div v-for="character in characters" :key="character.id" class="col-lg-4">
        <!-- 
            TODO: Añadir los datos de la ficha para completarla:

            - Nombre
            - Estado
            - Especie
            - Genero
            - Origen
            ...Resto de datos

            Para que quede una card al estilo: https://rickandmortyapi.com/

            Se añade card de ejemplo usando Bootstrap 5
         -->
        <div class="card mb-3">
            <div class="row g-0">
                <div class="col-md-4">
                <img src="" class="img-fluid rounded-start" alt="">
                </div>
                <div class="col-md-8">
                <div class="card-body">
                    <h5 class="card-title">Card title</h5>
                    <p class="card-text">This is a wider card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.</p>
                    <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p>
                </div>
                </div>
            </div>
        </div>
    </div>
</div>

</template>

<script>
export default {
    name: 'Character',
    data(){
        return {
            characters: [
                {
                    "id": 1,
                    "name": "Rick Sanchez",
                    "status": "Alive",
                    "species": "Human",
                    "type": "",
                    "gender": "Male",
                    "origin": {
                        "name": "Earth (C-137)",
                        "url": "https://rickandmortyapi.com/api/location/1"
                    },
                    "location": {
                        "name": "Earth (Replacement Dimension)",
                        "url": "https://rickandmortyapi.com/api/location/20"
                    },
                    "image": "https://rickandmortyapi.com/api/character/avatar/1.jpeg",
                    "episode": ["https://rickandmortyapi.com/api/episode/1", "https://rickandmortyapi.com/api/episode/2", "https://rickandmortyapi.com/api/episode/3", "https://rickandmortyapi.com/api/episode/4", "https://rickandmortyapi.com/api/episode/5", "https://rickandmortyapi.com/api/episode/6", "https://rickandmortyapi.com/api/episode/7", "https://rickandmortyapi.com/api/episode/8", "https://rickandmortyapi.com/api/episode/9", "https://rickandmortyapi.com/api/episode/10", "https://rickandmortyapi.com/api/episode/11", "https://rickandmortyapi.com/api/episode/12", "https://rickandmortyapi.com/api/episode/13", "https://rickandmortyapi.com/api/episode/14", "https://rickandmortyapi.com/api/episode/15", "https://rickandmortyapi.com/api/episode/16", "https://rickandmortyapi.com/api/episode/17", "https://rickandmortyapi.com/api/episode/18", "https://rickandmortyapi.com/api/episode/19", "https://rickandmortyapi.com/api/episode/20", "https://rickandmortyapi.com/api/episode/21", "https://rickandmortyapi.com/api/episode/22", "https://rickandmortyapi.com/api/episode/23", "https://rickandmortyapi.com/api/episode/24", "https://rickandmortyapi.com/api/episode/25", "https://rickandmortyapi.com/api/episode/26", "https://rickandmortyapi.com/api/episode/27", "https://rickandmortyapi.com/api/episode/28", "https://rickandmortyapi.com/api/episode/29", "https://rickandmortyapi.com/api/episode/30", "https://rickandmortyapi.com/api/episode/31", "https://rickandmortyapi.com/api/episode/32", "https://rickandmortyapi.com/api/episode/33", "https://rickandmortyapi.com/api/episode/34", "https://rickandmortyapi.com/api/episode/35", "https://rickandmortyapi.com/api/episode/36", "https://rickandmortyapi.com/api/episode/37", "https://rickandmortyapi.com/api/episode/38", "https://rickandmortyapi.com/api/episode/39", "https://rickandmortyapi.com/api/episode/40", "https://rickandmortyapi.com/api/episode/41"],
                    "url": "https://rickandmortyapi.com/api/character/1",
                    "created": "2017-11-04T18:48:46.250Z"
                },
                // ...
            ]
        }
    },
    methods:{
        getCaraters(){
            /* 
                TODO: Añadir la lógica necesaria para cargar los datos de los personajes de Rick and Morty atacando el endpoint
                https://rickandmortyapi.com/api/character y usando Axios*

                * Axios ya está instalado y configurado
            */
        }
    }
}
</script>

<style>

</style>