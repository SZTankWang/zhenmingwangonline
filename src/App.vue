<script  lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import Header from "./components/Header.vue"
import Body from "./components/Body.vue"

export default {
  components:{
    Header,
    Body
  }
}

</script>

<template>
 <Header/>
 <Body/>
</template>

<style>
body{
  width:100%;
  height:100vh;
  margin:0;
  background:#2b2a2a
}
</style>
