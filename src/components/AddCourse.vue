<template>
    <div style="padding: 5%;">
        <h2>Crear Curso</h2>
        <div class="form-group">
          <label type="text"  for="nombre" class="custom-label col-md-3">Nombre: </label>
          <input type="text" v-model="nombre" class="form-control" required/>
        </div>
        <div class="form-group">
          <label type="text"  for="nombre" class="custom-label col-md-3">Horas: </label>
          <input type="text" v-model="duracion" class="form-control" required/>
        </div>
        <button class="btn btn-primary" type="submit" @click="addCourse">Crear</button>
    </div>
</template>
   
<script>
    import axios from 'axios';

    export default {
      name: "AddCourse",
      data( ){
        return {
            nombre:"",
            duracion:"",
        }
      },
      methods: {
        addCourse: function(){
            axios.post("http://localhost:8080/profesor/crear-curso", {
                "courseName": this.nombre,
                "durationHours": this.duracion
            },{ params: { access_token: getAuthenticationToken() } }
            ).then( response => {
                    if( response.status !== 201 ){
                        alert( "Error en la creación del curso" );
                    }else{
                        alert("Curso creado");
                    }
            }).catch( error => {
                alert( 'Error en la petición' );
                console.log( error );
            } );   
        }
      }
  
    }
 </script>
  
<style scoped>
    .form-inline .form-group{
        margin-bottom: 1rem;
    }
</style>
