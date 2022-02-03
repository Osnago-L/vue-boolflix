<template>
  <div class="search-bar">
      <input :class="animationIsActive" placeholder="Search..." type="text" @keyup="$emit('search', searchValue )" v-model="searchValue">
      <img @click="startAnimation"  src="../../assets/img/magnifying-glass-solid.svg" alt="">
  </div>
</template>

<script>
export default {
    name: "SearchBar",
    data(){
        return{
            searchValue:"",
            animationIsActive:null
        }
    },
    methods:{
        startAnimation: function(){
            if(this.animationIsActive == null){
                this.animationIsActive = "width-grow-animation"
            }else if(this.animationIsActive == "width-grow-animation"){
                this.animationIsActive = "width-reduce-animation"
            }else{
                this.animationIsActive = "width-grow-animation"
            }
        }
    }

}
</script>

<style lang="scss" scoped>
.search-bar{
    display: flex;
    align-items: center;
    input{
        opacity: 0;
        width: 0px;
        height: 25px;
        padding: 0px 5px;
        border-radius: 10px 10px;
    }
    img{
        width: 18px;
        margin-left: 10px;
    }
}
</style>