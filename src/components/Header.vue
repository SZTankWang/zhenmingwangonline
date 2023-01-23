<script setup lang="ts">
import {onUnmounted, ref} from "vue"
import type {Ref} from "vue"
import moment from "moment"
import { onMounted } from "vue";

const time:Ref<string> = ref(getTime())
const interval:Ref<number|undefined> =ref(undefined);

onMounted(()=>{
    interval.value = setInterval(()=>{time.value=getTime()},0)
})

onUnmounted(()=>{
    clearInterval(interval.value);
})

function getTime():string{
    let now:moment.Moment = moment();
    return `${now.hour()}`+":"+`${now.minute()}`+":"+`${now.seconds()}`
}

</script>


<template>
<div class="header">
    <div class="row">
        <span class="color-font">
        Zhenming Wang
    </span>
    <span class="color-font time">{{ time }}</span>
    </div>
    <div class="row">
        <span>A website built with Vue</span>
    </div>
</div>
</template>

<style scoped>
@import "../index.css";
.header{
    height:fit-content;
    display: flex;
    flex-direction: column;
    /* justify-content: space-between; */
    padding:0.5rem;
    /* width:96vw; */
    top:0;
    z-index:2;
    background-color: #2b2a2a;
    /* position:relative; */
    animation-name:slide-up;
    animation-duration: 800ms;
    animation-timing-function: ease;
}

@keyframes slide-up {
    from{
        transform:translateY(1rem);
        opacity:0;
    }
    to{
        /* transform:translateY(0); */
        opacity:1;
    }
}
.time{
    position:absolute;
    right:0;
}
.color-font{
    flex-basis:fit-content;
    display: inline-block;
    font-size:1.7rem;
    font-family:sans-serif ;
    font-weight:500;
    background:linear-gradient(90deg, rgba(63,94,251,1) 0%, rgba(252,70,107,1) 100%);
    color:transparent;
    -webkit-background-clip:text;
    
}

</style>