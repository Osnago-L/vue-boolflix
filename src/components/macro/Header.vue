<template>
  <div class="header">
    <img src="../../assets/img/Logonetflix.png" alt="">
    <div class="buttons">
      <img src="../../assets/img/user-solid.svg" alt="">
      <SearchBar class="search-bar" @search="searchedValue"
      />
    </div>
  </div>
</template>

<script>

import SearchBar from "../commons/SearchBar.vue";
export default {
    name: "Header",
    components:{
      SearchBar
    },
    methods:{
      searchedValue: function(searchValue){
        this.$emit('search', searchValue )
      }
    }
}
</script>

<style lang="scss" scoped>
@import "../../assets/style/partial/variables.scss";

.header{
  height: $header-height;
  padding: 0 20px;
  background-color: black;
  color:red;

  display: flex;
  align-items: center;
  justify-content: space-between;

  &>img{
    width:80px
  }
}

.buttons{
  display: flex;
  gap: 10px;
  img{
    width: 18px;
  }
}

</style>