<template lang="html">
  <div class="container">
    <div class="row">
      <div class="col text-left">
        <h2>Listado de libros</h2>
        <div class="col-md-12">
          <b-table striped hover :items="books" :fields="fields">
              <template v-slot:cell(action)="row" >
                <b-button size="sm" variant="primary" :to="{ name:'EditBook', params: {bookId: row.item.id} }">
                  Editar
                </b-button>
                <b-button size="sm" variant="danger" :to="{ name:'DeleteBook', params: {bookId: row.item.id} }">
                  Eliminar
                </b-button>
              </template>
          </b-table>
          <div v-show="books.length<=0">
            <b-alert show variant="warning">
              No hay libros disponibles
            </b-alert>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
  import * as config from '../../base.js';
    export default {
        name: "ListBook.vue",
        data(){
            return {
                fields:[
                    { key: 'title', label: 'Título'},
                    { key: 'description', label: 'Descripción'},
                    { key: 'action', label: 'Actions' }
                ],
                books:[]
            }
        },
        created(){
            this.getBooks();
        },
        methods:{
            getBooks(){
                let route = config.base_path+'api/v1.0/books';

                axios.get(route).then((res)=>{
                        this.books = res.data
                    }).catch((err)=>{
                        console.log(err);
                    })
            }
        }
    }
</script>

<style scoped>

</style>
