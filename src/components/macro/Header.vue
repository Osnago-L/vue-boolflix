<template>
  <div class="header">
    <div>NETFLIX LOGO</div>
    <SearchBar/>
  </div>
</template>

<script>

import SearchBar from "../commons/SearchBar.vue";
export default {
    name: "Header",
    components:{
      SearchBar
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
}

</style>