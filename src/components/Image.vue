<script setup lang="ts">
defineProps({
    url:String,
    width:String,
    height:String
})

</script>

<template>
<div 
    class="image" 
    :style="{
        backgroundImage:`url(${url})`,
        width:`${width}rem`,
        height:`${height}rem`

}">

</div>

</template>    

<style scoped>
.image{
    padding:0.3rem;
    border-radius: 0.2rem;
    margin-top:0.2rem;
    background-size:cover;
}
</style>