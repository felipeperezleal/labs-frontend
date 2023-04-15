<template>
  <div class="container-fluid mt-2">
    <h1>Bienvenido al dummy</h1>
    <button type="button" class="btn btn-outline-primary" style="margin: 1%;" @click="addCourse" v-if="this.profesor">Nuevo curso</button>
    <button type="button" class="btn btn-outline-primary" style="margin: 1%;" @click="courses" >Mis cursos</button>
    <button type="button" class="btn btn-outline-primary" style="margin: 1%;" @click="addRole" >Nuevo rol</button>
    <button type="button" class="btn btn-outline-primary" style="margin: 1%;" @click="roles" >Roles</button>
    <div class="row">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  import {getAuthenticationToken} from '@/dataStorage';

  export default{
    name: "Home",
    data(){
      return{
        misroles: null,
        profesor: false
      }
    },
    beforeCreate( ){
      if( !getAuthenticationToken( ) ){this.$router.push({name: 'login'})}
    },
    mounted: function(){
      axios.get(this.$store.state.backURL+'', {
          params: { access_token: getAuthenticationToken( )}
        })
        .then(response => {
            this.misroles = response.data;
            for (const rol of this.misroles) {
              if(rol.id === 2){
                this.profesor = true;
                break;
              }
            }
        });
    },
    methods:{
      addCourse: function(){
        this.$router.push("/profesor/nuevo-curso")
      },
      courses: function(){
        this.$router.push("/mis-cursos")
      },
      addRole: function(){
        this.$router.push("/principal/nuevo-rol")
      },

      roles: function(){
        this.$router.push("/principal/roles")
      },
    }
  }
</script>

<style>

</style>
