<template>
  <div class="search-bar">
      <input type="text" @keyup="$emit('search', searchValue )" v-model="searchValue">
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
    margin: 5px 10px;
}
</style>