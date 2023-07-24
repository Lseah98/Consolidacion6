<template>
    <div id="Juegos">
        <h1>Componente Juegos</h1>
        <div class="contenedorPadre">
            <div v-for = "(juego,index) in juegos" class="card m-2" style="width: 18rem;">
                    <img v-bind:src="juego.background_image" class="card-img-top" alt="...">
                    <div class="card-body">
                        <h5 class="card-title">{{ juego.name }}</h5>
                        <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
                    </div>
                    <ul class="list-group list-group-flush">
                        <li class="list-group-item">Rating: {{ juego.rating }}</li>
                        <li class="list-group-item">Released: {{ juego.released }}</li>
                        <li class="list-group-item">Updated: {{ juego.updated }}</li>
                    </ul>
                    <div class="card-body">
                        <a v-on:click="mostrarOpiniones(juego.name)" class="btn btn-primary">Opinar</a>
                        <a href="#" class="card-link">Another link</a>
                    </div>
            </div>
        </div>
    </div>

</template>

<script>
import axios from 'axios';
export default{
    name: 'Juegos',
    data: function(){
        return{
            cantidadJuegos:0,
            juegos:[],

        }
    },
    methods:{
        consumirAPI:function(){
            let url= 'https://api.rawg.io/api/games?key=eea01750c4b24c1db7a151add37c6166';
            axios(url)
                .then(respuesta=>{
                    //console.log(respuesta);
                    console.log(respuesta.data.results[9].name);
                    this.cantidadJuegos = respuesta.data.results.length;

                    for(let i=0; i<respuesta.data.results.length; i++){
                        this.juegos.push(respuesta.data.results[i]);
                    }
                    console.log(this.juegos[0]);

                })
                .catch(error=>{
                    console.log(error);
                })

        },
        mostrarOpiniones:function(nombreJuego){
            this.$router.push(`/opiniones/${nombreJuego}`);

        }

    },
    created(){
        this.consumirAPI();

    }
}
</script>

<style scoped>
#Juegos{
    background-color: darksalmon;
}
.contenedorPadre{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}

</style>