<template>
    <ul class="news__list">

<!-- 
        <li v-for="(article,index) in articles" :key=index  class="news__item">
            {{article.title}}
        </li> -->

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
    </ul>
</template>

<script>
export default {
    data() {
      return {
          articles: []
      }        
    },
    created(){
        fetch('https://newsapi.org/v2/top-headlines?country=us',{
            headers:{
                'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
            }
        }).then((response)=>{
            return response.json();
        }).then((data)=>{
            console.log(data);
            this.articles = data.articles;
            })
    }
}
</script>


<style>
/* Add any component specific styles here */
</style>