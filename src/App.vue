<template>
  <div id="app">
    <Header @search="searchedValue"
    />
    <Main :search="dataSearchValue"/>
  </div>
</template>

<script>
import Header from "./components/macro/Header.vue"
import Main from "./components/macro/Main.vue"

export default {
  name: 'App',
  components: {
    Header,
    Main
  },
  data(){
    return{
      dataSearchValue:""
    }
  },
  methods:{
    searchedValue:function(searchValue){
      this.dataSearchValue=searchValue;
    }
  }
}
</script>

<style lang="scss">
@import "./assets/style/global.scss";

</style>
