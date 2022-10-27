<template>

  <section class="src-components-usuarios">
   <div class="jumbotron">
    <h1>Metodo POST</h1>
      <button class="btn btn-success my-3 mr-3" @click="getPostXHR()">XMLHttpRequest</button>
      <button class="btn btn-success my-3 mr-3" @click="getPostsFetch()">Fetch</button>
      <button class="btn btn-success my-3 mr-3" @click="getPostsAxios()">Axios</button>
      <button class="btn btn-warning my-3 mr-3" @click="borrar()">borrar</button>


      <!----------------------TABLA--------------------------------------------------------------->
      <div>
      <table class="table table-dark">
          <tr>
            <th>Nombre</th>
            <th>Email</th>
            <th>Telefono</th>
          </tr>
          <tr v-for="usuario in usuarios" :key="usuario.email ">
            <td>{{usuario.nombre }}</td>
            <td>{{ usuario.email }}</td>
            <td>{{ usuario.telefono }}</td>
          </tr>
        </table>
      </div>
   </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-components-usuarios',
    props: [],
    mounted () {
    
    },
    data () {
      return {
      ruta:"https://6351ddd1dfe45bbd55ca4dfa.mockapi.io/usuarios",
      usuarios:[]
      }
    },
    methods: {
      async getPostsAxios() {
        try {
          let post = await this.axios(this.ruta)
          this.usuarios = post.data
        }
        catch(error) { console.error(error) } 

      },
      borrar(){
        this.usuarios=[]
      },xhrPromise() {
        return new Promise((resolve,reject) => {
          const xhr = new XMLHttpRequest()
          xhr.open('get', this.ruta)
          xhr.addEventListener('load', () => {
            if(xhr.status == 200) {
              let respuesta = JSON.parse(xhr.response)
              resolve(respuesta)
            }
            else {
              reject(`Error http: ${xhr.status}`)
            }
          })
          xhr.send()
        })
      },
      async getPostXHR() {
          try {
            let post = await this.xhrPromise()
            this.usuarios = post
          }
          catch(error) {
            console.error(error)
          }
      },
      async getPostsFetch() {
        try {
          let response = await fetch(this.ruta)
          console.log(response)
          let respuesta = await response.json()
          this.usuarios = respuesta
        }
        catch(error) {
          console.error(error)
        }
      }

        },
    computed: {

    }
}


</script>

<style scoped lang="css">
.jumbotron{
  background-color: red;
  color: black;
}
</style>
