<script  lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import Header from "./components/Header.vue"
import Body from "./components/Body.vue"
import Footer from './components/Footer.vue'

export default {
  components:{
    Header,
    Body,
    Footer 
  }
}

</script>

<template>
 <Header/>
 <Body/>
 <Footer/>
</template>

<style>
body{
  width:100%;
  height:100vh;
  margin:0;
  background:#2b2a2a;
  /* transition:all 0.4s ease; */
}
</style>
