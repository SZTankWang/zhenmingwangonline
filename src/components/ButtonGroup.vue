<script setup lang="ts">
import { computed, type ComputedRef,reactive} from '@vue/reactivity';
import { nanoid } from 'nanoid';
import { onBeforeMount } from 'vue';

interface ButtonGroup {
    text:string,
    value:string,
    id?:string,
    active?:boolean
}

const props = defineProps<{
    elements:ButtonGroup[],
    defaultActive:string
}>()

const fullProp:ComputedRef<ButtonGroup[]> = computed(()=>
     props.elements.map(e=>{
        e.id = id();

        e.text===props.defaultActive?
        e.active = true:
        e.active = false
        ;
        return e;
    })
)

const reactiveProp = reactive<ButtonGroup[]>([])

const id:()=>string = ():string=>nanoid(5)


const emits = defineEmits<{
    (e:"switch-function",value:string):void
}>()

const onClick = (e:Event):void=>{
    const clicked = (e.target as HTMLElement).innerHTML;
    reactiveProp.forEach(p=>{
        if(p.active === true){
            p.active = false;
        }
        if(p.text===clicked){
            p.active = true;
            emits("switch-function",p.value)
        }
    })

}

onBeforeMount(()=>{
    fullProp.value.map(e=>reactiveProp.push(e))
})

</script>


<template >

<span v-for="i in reactiveProp" 
    :key="i.id" 
    class="button" 
    :class="{active:i.active}"
    @click="onClick">
    {{ i.text }}
</span>

</template>

<style scoped>

.button{
    padding:0.1rem;
    background-color:#2b2a2a;
    border-radius:3px;
    border:1px solid #F3bc21;
    transition:all 400ms;
    margin-left:0.3rem;
    cursor:pointer
}

.active{
    border:transparent;
    color:#2b2a2a;
    background-color:#F3bc21;
    transition:all 400ms;
}
</style>