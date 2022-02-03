<template>
  <div class="main" >
    <h1>Movies</h1>
    <div class="cleangrid">
      <MainCard v-for="element,index in moviesList" :key="index" :dataObj="element"
      />
    </div>
    <h1>Series</h1>
    <div class="cleangrid">
      <MainCard v-for="element,index in tvList" :key="index" :dataObj="element"
      />
    </div>
  </div>
</template>

<script>
import MainCard from "../commons/MainCard.vue"

import axios from 'axios'


export default {
    name: "Main",
    components:{
      MainCard
    },
    props:{
      search:String
    },
          data () {
        return {
            moviesList: [],
            tvList:[],
            selected:"The"
        }
    },
    methods:{
        getMovies: function(){
                axios.get('https://api.themoviedb.org/3/search/movie', {
                    params: {
                    api_key: "abebf56715261d00da812031b9c3e2ed",
                    query: this.selected
                    }
                    })
                    .then((apiData) =>{
                        this.moviesList = apiData.data.results;
                    })
                    .catch(function (error) {
                        console.log(error);
                    })
                    .then(function () {
                        // always executed
                    });  
        },
        getTv: function(){
                axios.get('https://api.themoviedb.org/3/search/tv', {
                    params: {
                    api_key: "abebf56715261d00da812031b9c3e2ed",
                    query: this.selected
                    }
                    })
                    .then((apiData) =>{
                        this.tvList = apiData.data.results;
                    })
                    .catch(function (error) {
                        console.log(error);
                    })
                    .then(function () {
                        // always executed
                    }); 
        },
        filterArray: function(){
          this.search == "" ? this.selected = "The" : this.selected = this.search
          this.getMovies()
          this.getTv()
        }
    },
    created: function(){
        this.getMovies()
        this.getTv()
    },
    watch:{
      search: function(){
        this.filterArray()
      }
    },
    computed:{
      watcher(){
        return this.selected
      }
    }
}
</script>

<style lang="scss" scoped>
@import "../../assets/style/partial/variables.scss";
.main{
  padding: 30px 30px;
  .cleangrid{
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    margin: 20px 0;
  }
}
</style>