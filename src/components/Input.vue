<script setup lang="ts">
import { computed, type ComputedRef } from '@vue/reactivity';
import { nextTick, onMounted,ref, watch } from 'vue';
import type {Ref} from "vue"

type Fn = (...args:any[])=>void;


const props = defineProps<{
    width:string,
    height:string,
    fn:string
}>()

const emit = defineEmits<{
    (e:"spawntext",value:string):void
}>()

const inputValue:Ref<string|undefined> = ref(undefined)
const fnRef:Ref<(...args:any[])=>void> = ref(()=>null);

const emitTextSpawn = ():void=>{
    if(inputValue.value !== undefined){
        console.log("emit")
        emit("spawntext",inputValue.value)
    }
}

const getValue = async (e:Event):Promise<void>=>{
    e.preventDefault();
    inputValue.value = (e.target as HTMLDivElement).innerText
    await nextTick();
    //emit event 
    emitTextSpawn();
}

//onmounted
onMounted(():void=>{
    //event listener for keydown
    fnRef.value = debounce(getValue,2000)
    document.getElementById("debounce-input")?.addEventListener("keydown",fnRef.value)

})

function debounce(fn:Fn,delay:number):Fn{
    let timer:null|number=null;

    return (...args:any[])=>{
        if(timer !== null){
            //a previous timer exist, clear the timeout and start a new one
            clearTimeout(timer)
        }
            timer = setTimeout(()=>{
                fn.apply(null,args)
            },delay)
        
    }
}

function throttle(fn:Fn,delay:number):Fn{
    //when we start typing, start the timer. So the event
    //is triggered within a fixed interval
    let timer:null|number = null;
    return (...args:any[])=>{
        if(timer === null){
        //previous function has been executed
        timer = setTimeout(()=>{
            fn.apply(null,args)
            timer = null;
        },delay)
        }

    }
}

//watch prop change
watch(props,(newProp,oldProp)=>{
    const input = document.getElementById("debounce-input")
    //clear previous event listener
    input!.removeEventListener("keydown",fnRef.value)    
    //add new event listener using the new Fn
    if(newProp.fn === "debounce"){
        fnRef.value = debounce(getValue,2000)
    }
    else{
        fnRef.value = throttle(getValue,2000)
    }
    input!.addEventListener("keydown",fnRef.value)   
})

</script>


<template>
<div 
class="input"
id="debounce-input"
contenteditable="true"
:style="{minWidth:`${width}rem`
        ,minHeight:`${height}rem`
        }"
autofocus

>

    
</div>

</template>

<style scoped>
.input{
    background:transparent;
    font-size:1.3rem;
    padding-bottom:0.1rem;
}

.input:focus{
    outline:none;
    border-bottom:1px solid #F3bc21;
    transition:all 300ms ease;
}

</style>