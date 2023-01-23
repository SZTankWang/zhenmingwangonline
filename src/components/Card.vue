<script setup lang="ts">
    defineProps({
        title:String,
        width:String,
        height:String
    })
</script>

<template>
    <div 
    class="card"
    :style="{minWidth:`${width}rem`,minHeight:`${height}rem`}"
    >
        <div class="card-row title">
            {{ title }}
        </div>
        <div class="card-row">
            <slot></slot>
        </div>
    </div>
</template>    


<style scoped >
@import '../index.css';
.title{
    color:#2b2a2a;
    border-bottom:0.1rem solid #ebe9e9
}

.card{
    display: flex;
    flex-direction: column;
    min-height:6rem;
    background:#ffffff;
    padding:0.5rem;
    position:relative;
    border-radius: 0.3rem;
    margin:1rem;
}



</style>