<script setup lang="ts">
import { onMounted,onUpdated,ref,watch,type Ref } from 'vue';
import { computed } from '@vue/reactivity';
const props = defineProps<{
    value:string|undefined,
    id:string|undefined
}>();
const idRef:Ref<string|undefined> = ref<string|undefined>(undefined)
const animate:Ref<boolean> = ref<boolean>(false)



onUpdated(()=>{
    // console.log("update",props.id)
    idRef.value = props.id;
})

watch(idRef,(newId,prevId)=>{
    animate.value = newId !== prevId
    setTimeout(()=>animate.value = false,500)
    })
</script>


<template>
<div class="float" :class="{fadeIn:animate}">
    <p v-if="props.value!==undefined">{{props.value}}</p>
    <p v-else>开始键入...</p>
</div>
</template>

<style scoped>

.float{
    /* font-size:2em; */
    color:#2b2a2a;
    position:absolute;
    font-family: sans-serif;
    left:1rem;
    background:#F3bc21;
    margin-top:0.2rem;
    border-radius:3px;
}

.fadeIn{
    animation-name:fade-in;
    animation-duration: 400ms;

}
@keyframes fade-in {
    from{
        opacity:0;
    }
    to{
        opacity:1;
    }
    
}

p{
    margin:0;
}
</style>