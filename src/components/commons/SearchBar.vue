<template>
  <div class="search-bar">
      <input placeholder="Search..." type="text" @keyup="$emit('search', searchValue )" v-model="searchValue">
  </div>
</template>

<script>
export default {
    name: "SearchBar",
    data(){
        return{
            searchValue:""
        }
    },

}
</script>

<style lang="scss" scoped>
.search-bar{
    margin: 10px 0px;
}
</style>