<script setup lang="ts">
interface cardProps {
        title:string,
        width:string,
        height:string,
        onclick?:(v:string)=>void

}

const props = withDefaults(defineProps<cardProps>(),{
    onclick:()=>{}
})
</script>

<template>
    <div 
    class="card"
    :style="{minWidth:`${width}rem`,minHeight:`${height}rem`}"
    @click="props.onclick"
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
    animation-name:fade-in;
    animation-duration: 300ms;
    cursor:pointer;
}

@keyframes fade-in {
    from{
        opacity:0;
    }

    to{
        opacity:1;
    }
}



</style>