<template>
  <div id="app">
  <img src="@/assets/images/bg-desktop-light.jpg" alt="header-pic">
  <app-todo></app-todo>
  </div>
</template>

<script>
import todoList from '@/components/todoList.vue/';
export default {
  components: {
   'app-todo':todoList,
  }
}
</script>

<style scoped>
* {
 margin:0;
 padding:0;
 }
 img {
   margin-top:-0.5rem;
   margin-left:-0.5rem;
   position:relative;
   display:inline-block;
   }
@media(max-width:768px){
   img{
    width:375px;
    height:250px;
    }
  }
</style>
