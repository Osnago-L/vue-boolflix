<template>
  <div class="main-card">
    <div>
      <div class="titles">
        <span class="title">{{switchCategory()}}</span>
        <span v-if="dataObj.original_title" class="original_title">{{dataObj.original_title}}</span>
      </div>
      <div class="lang-vote">
        <div>        
          <span class="language">{{dataObj.original_language}}</span>
          <img class="flags" v-if="dataObj.origin_country" :src="getFlags()" alt="">
        </div>    
        <div class="vote" >
          <img class="stars" v-for="element,index in roundVote()" :key="index" src="../../assets/img/star-solid.svg" alt="">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    name: "MainCard",
    props:{
      dataObj:Object
    },
    methods:{
      getFlags: function(){
       let country = this.dataObj.origin_country[0]?.toLowerCase() || 'un'
       return "https://flagcdn.com/w20/"+ country +".png"
      },
      switchCategory: function(){
        if(this.dataObj.title == undefined){
          return  this.dataObj.name
        }else{
          return this.dataObj.title
        }
      },
      roundVote:function(){
        return Math.round(this.dataObj.vote_average/2)
      }
    },
    created:function(){
       this.switchCategory()
    },
    watch:{
      dataObj: function(){
        this.switchCategory()
      }
    }
}
</script>

<style lang="scss" scoped>
.main-card{

  &>div{
    width: 200px;
    height: 200px;
    border: 1px solid black;
    padding: 10px;

    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  .titles{
    display: flex;
    flex-direction: column;

  .title{
    font-weight: bold;
  }
  .original_title{
    font-style: italic;
    font-size: 13px;
  }

  }

  .lang-vote{
    display: flex;
    justify-content: space-between;
  }
  
  .language{
    padding: 3px;
    margin-right: 5px;
    background-color: black;
    font-weight: bold;
    color: white;
    text-transform: uppercase;
    border-radius: 5px 5px;

  }
    .flags{
    border: 0.5px solid rgba(0, 0, 0, 0.15);
  }

  .vote{
    display: flex;

    .stars{
      width:13px;
    }
  }
}
</style>