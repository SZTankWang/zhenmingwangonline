<script setup lang="ts">
import Card from "./Card.vue"
import Image from "./Image.vue"


</script>


<template>
<div class="body">

<div class="row">
<Card 
title="A Todo App"
width="18"
height = "10"
>
    <div class="col">
        <Image
         url="src/assets/vue.png"
         width="5"
         height="5"

         />
<div class="text">
    Built with Vue, Vue Router, Pinia, MongoDB.
    
</div>

    </div>
</Card>

<Card
title="A Grid Editor"
width="18"
height="10"
>
<div class="col">
    <Image
    url="src/assets/react.png"
    width="5.9"
    height="5.1"
    />
<div class="text">
    Built with React + Redux
</div>
</div>
</Card>
</div>

</div>

</template>

<style scoped>
@import "../index.css";

.body{
    margin-top:2rem;
    padding:1rem;
    /* background:#2b2a2a */
}

.title{
    font-size:1.3rem
}

</style>