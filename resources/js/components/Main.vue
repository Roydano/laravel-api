<template>
  <main>
      
    <div class="container">
        <div class="row justify-content-between">
            <div class="col-md-4" v-for="post in posts" :key="post.id">

                <div class="card text-dark bg-info my-5 mx-3" style="max-width: 18rem;">
                    <div class="card-header text-center">{{ post.title }}</div>
                    <div class="card-body">
                        <h5 class="card-title">{{ post.author }}</h5>
                        <span><i>{{ formatoData( post.updated_at ) }}</i></span>
                        <hr>
                        <p class="card-text">{{ post.description }}</p>
                    </div>
                    <button class="btn btn-button">Dettagli</button>
                </div>

            </div>
        </div>
    </div>
      
  </main>
</template>

<script>
export default {
    name: "Main",
    data(){
        return {
            postUrl: 'http://127.0.0.1:8000/api/posts',
            posts: []
        }
    },
    created(){
        this.getPosts();
    },
    methods:{
        getPosts(){
            axios.get(this.postUrl)
            .then(response => {
                console.log(response.data.result);
                this.posts = response.data.result;
            })
            .catch();
        },
        formatoData(date){
            const data = new Date(date);

            return data.getDate() + '/' + data.getMonth() + '/' + data.getFullYear();
        }
    }

}
</script>

<style lang="scss" scoped>

    main{
        background-color: rgb(218, 218, 218);

        .card{
            box-shadow: 2px 2px 2px 2px rgb(117, 117, 117);

            .card-header{
                font-size: 20px;
                color: white;
            }
    
            .card-body{
                background-color: white;
    
                .card-title{
                    display: -webkit-box;
                    -webkit-box-orient: vertical;
                    -webkit-line-clamp: 1; 
                    overflow: hidden;
                }
    
                .card-text{
                    display: -webkit-box;
                    -webkit-box-orient: vertical;
                    -webkit-line-clamp: 3; 
                    overflow: hidden;
                }
            }
    
            button{
                color: white;
            }
        }


    }


</style>