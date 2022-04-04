<template>
    <form action="" @submit.prevent="searchNews" class="d-flex flex-column justify-content-center">
        <div class="input-group mx-sm-3 mb-2">
            <label class="visually-hidden" for="search">Search</label>
            <input type="search" name="search" v-model="searchTerm" id="search" 
            class="form-control mb-2 mr-sm-2" placeholder="Enter Search Term Here">
            <button class="btn btn-primary mb-2">Search</button>
        </div>
        <p>You are searching for{{searchTerm}}</p>
    </form>

    <div class="container">
        <div class="row">
            <div class="col-3 pb-4 news__item" v-for="(article,index) in articles" :key=index>
                <div class="card">
                    <img class="card-img-top" :src="article.urlToImage" :alt="article.title" srcset="">
                    <div class="card-body">
                        <h5 class="card-title">
                            {{article.title}}
                        </h5>
                        <p class="pb-1 text muted">
                            {{article.content}}
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
      return {
          articles: [],
          searchTerm:''
      }        
    },
    methods:{
        searchNews(){
            fetch('https://newsapi.org/v2/everything?q='+
                this.searchTerm + '&language=en', {
                    headers: {
                        'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`,
                    }
                }).then((response)=>{
                    return response.json();
                }).then((data)=>{
                    // console.log(data);
                    this.articles = data.articles;
                })
        }
    }
    //  created(){
    //     fetch('https://newsapi.org/v2/top-headlines?country=us',{
    //         headers:{
    //             'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
    //         }
    //     }).then((response)=>{
    //         return response.json();
    //     }).then((data)=>{
    //         console.log(data);
    //         this.articles = data.articles;
    //         })
    // }

}
</script>


<style>
/* Add any component specific styles here */
</style>