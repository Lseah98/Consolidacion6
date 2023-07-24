<template>
    <div id="OpinionesView">
        <h1>Componente OpinionesView</h1>
        <p>Opina sobre {{ nombre }}</p>
        <hr>
        <div class="container" id="divForm">
            <div class="mb-3 m-2">
            <label for="txtNombre" class="form-label">Nombre:</label>
            <input type="text" class="form-control" id="txtNombre" v-model="nombreEnviar">
            </div>
            <div class="mb-3 m-2">
            <label for="txtOpinion" class="form-label">Escriba su opinion</label>
            <input type="text" class="form-control" id="txtOpinion" v-model="opinionEnviar">
            </div>
            <button type="submit" v-on:click.prevent="agregarOpinion" class="btn btn-primary m-2">Agregar</button>
        </div>
        <hr>
        <h2>A continuacion podras ver tu opinion</h2>
        <div id="sinOpiniones" class="m-3" v-if="cantidadOpiniones<1">
            <p>No existen opiniones para mostrar</p>
        </div>
        <hr>


        <div class="accordion" id="acordeonOpiniones" v-if="cantidadOpiniones>0">
                <div class="accordion-item m-2" v-for="(elemento,index) in opiniones">
                    <h2 class="accordion-header">
                    <button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#collapseOne" aria-expanded="true" aria-controls="collapseOne">
                        Opinion creada por : {{ elemento.nombre }}
                    </button>
                    </h2>
                        <div id="collapseOne" class="accordion-collapse collapse show" data-bs-parent="#accordionExample">
                            <div class="accordion-body m-2" id="cuadroOpinion">
                            {{ elemento.opinion }}
                            </div>
                                <button class="btn btn-danger m-2">Eliminar</button>
                                <button class="btn btn-warning m-2">Editar</button>
                        </div>

                </div>
        </div>

        <router-link to="/">Volver</router-link>
    </div>
</template>

<script>
export default{
    name:'OpinionesView',
    props:['nombre'],
    data: function(){
        return{
            cantidadOpiniones: 0,
            nombreEnviar: '',
            opinionEnviar: '',
            opiniones:[],


        }
    },
    methods:{
        agregarOpinion: function(){
            this.cantidadOpiniones++;
            let nuevaOpinion={
                nombre: this.nombreEnviar,
                opinion: this.opinionEnviar,
            };
            this.opiniones.push(nuevaOpinion)


        }

    }
}
</script>

<style scoped>
#OpinionesView{
    background-color: aqua ;
}
#divForm{
    background-color: bisque;
    text-align: left;
}
#sinOpiniones{
    border: 1px solid red;
    background-color: lightcoral;
    color:black;
}
#acordeonOpiniones{
    text-align: left;
    background-color: bisque;
}

</style>