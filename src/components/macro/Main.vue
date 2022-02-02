<template>
  <div class="main" >
    <SearchBar  @search="filterArray"/>
    <div>
      <MainCard v-for="element,index in moviesList" :key="index" :dataObj="element"
      />
    </div>
  </div>
</template>

<script>
import SearchBar from "../commons/SearchBar.vue"
import MainCard from "../commons/MainCard.vue"

import axios from 'axios'


export default {
    name: "Main",
    components:{
      MainCard,
      SearchBar
    },
          data () {
        return {
            moviesList: [],
            filteredMovies: [],
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
        filterArray: function(searchValue){
          this.selected = searchValue
          this.getMovies()
        }
    },
    created: function(){
        this.getMovies()
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
  div{
    display: flex;
    flex-wrap: wrap;
  }
}
</style>