<template>
  <div class="main-card">
    <div>
      <span class="title">{{dataObj.title}}</span>
      <span class="original_title">{{dataObj.original_title}}</span>
      <span class="language">{{dataObj.original_language}}</span>
      <span class="vote">{{dataObj.vote_average}}</span>
    </div>
  </div>
</template>

<script>
export default {
    name: "MainCard",
    props:{
      dataObj:Object
    }
}
</script>

<style lang="scss" scoped>
.main-card{

  div{
    width: 200px;
    height: 200px;
    margin: 10px 10px;
    border: 1px solid black;
    padding: 10px;

    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: repeat(4,1fr);
  }
  .title{
    font-weight: bold;
  }
  .original_title{
    font-style: italic;
    font-size: 13px;
  }

  .language{
    
    text-transform: uppercase;

  }
  .vote{
    font-weight: bold;
  }
}
</style>