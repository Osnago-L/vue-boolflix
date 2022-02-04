<template>
  <div class="main container" >
    <h1>Movies</h1>
    <!-- SECTION WITH OVERLAYS -->
    <section>
      <!-- OVERLAY LEFT  -->
      <div class="overlay_left">
        <div @mouseover="scrollLeft" @mouseleave="stopScroll" class="arrow_left">&#8592;</div>
      </div>
      <!-- CARDS -->
      <div id="movies" class="cleangrid">
      <MainCard v-for="element,index in moviesList" :key="index" :dataObj="element"
      />
      </div>
      <!-- OVERLAY RIGHT  -->
      <div class="overlay_right">
        <div @mouseover="scrollRight" @mouseleave="stopScroll" class="arrow_right">&#8594;</div>
      </div>
    </section>

    <h1>Series</h1>
    <section>
      <div class="overlay_left">
        <div @mouseover="scrollLeft" @mouseleave="stopScroll" class="arrow_left">&#8592;</div>
      </div>
      <div id="series" class="cleangrid">
        <MainCard v-for="element,index in tvList" :key="index" :dataObj="element"
        />
      </div>
      <div class="overlay_right">
         <div @mouseover="scrollRight" @mouseleave="stopScroll" class="arrow_right">&#8594;</div>
      </div>
    </section>
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
            selected:"The",
            interval:null
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
        },
        scrollRight: function(event){
          this.interval = setInterval(() => {
            event.path[2].querySelector(".cleangrid").scrollLeft += 30
          }, 100);
          
        },
        scrollLeft: function(event){
          this.interval = setInterval(() => {
            event.path[2].querySelector(".cleangrid").scrollLeft -= 30
          }, 100);
          
        },
        stopScroll: function(){
          clearInterval(this.interval)
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
  background-color: #141414;
  padding-top: 20px;
  color: #e5e5e5;

  section{
    position: relative;

    .overlay_right,.overlay_left{
      position: absolute;
      z-index: 999;
      width: 60px;
      height: 94%;

      display: flex;
      align-items: center;
    }
    .overlay_left{
      top: 20px;
      left: 0;
      background: linear-gradient(to right, black,transparent);

      .arrow_left{
         display: flex;
         align-items: center;
         background-color: #141414c7;
         width: 40px;
         height: 80px;
         border-top-right-radius: 80px;
         border-bottom-right-radius: 80px;

         padding-left: 5px;
       }
    }
    .overlay_right{
      justify-content: end;
      top: 20px;
      right: 0;
      background: linear-gradient(to left, black,transparent);

      .arrow_right{
         display: flex;
         align-items: center;
         justify-content:end;
         background-color: #141414c7;
         width: 40px;
         height: 80px;
         border-top-left-radius: 80px;
         border-bottom-left-radius: 80px;

         padding-right: 5px;
       }
    }
  }

  .cleangrid{
    display: flex;
    overflow-x: auto;
    gap: 5px;
    padding: 20px 0;

  }
}
</style>