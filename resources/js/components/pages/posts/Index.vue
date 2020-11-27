<template>
    <div>
        <h1>Все записи</h1>
        <div v-if="errored" class="alert alert-danger" role="alert">
            Записи не загрузились
        </div>
        <table v-else class="table">
            <div v-if="loading">Loading...</div>
            <thead>
            <tr>
                <th scope="col">ID</th>
                <th scope="col">Name</th>
                <th scope="col">Описание</th>
                <th scope="col"></th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="post in posts":key="post.id">
                <th>{{post.id}}</th>
                <td>{{post.title}}</td>
                <td>{{post.description}}</td>
                <td>
                    <button class="btn btn-success">Редактировать</button>
                    <button class="btn btn-danger">Удалить</button>
                </td>
            </tr>
            </tbody>
        </table>
    </div>
</template>
<script>
    export default {
        data(){
            return{
                posts:[],
                post:{
                    id:'',
                    title:'',
                    description:'',
                },
                post_id:'',
                pagination:{},
                edit:false,
                loadig:true,
                errored:false
            }
        },
        mounted () {
            this.getPosts()
        },
        methods:{
          getPosts(){
              axios
                  .get('/api/posts')
                  .then(response => this.posts = response.data.data)
                  .catch(error=>{
                      console.log(error)
                      this.errored = true;
                  })
                  .finally(()=>this.loading = false)
          }
        }
    }
</script>


