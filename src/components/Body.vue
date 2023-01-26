<script setup lang="ts">
import { ref,type Ref } from "vue";
import Card from "./Card.vue"
import Image from "./Image.vue"
import Input from "./Input.vue"
import FloatingText from "./FloatingText.vue";
import ButtonGroup from "./ButtonGroup.vue"
import {nanoid} from "nanoid";

const spawnText:Ref<undefined|string> =ref<undefined|string>(undefined)
const spawnTextId:Ref<undefined|string> = ref<undefined|string>(undefined)
const selectedFn:Ref<string> = ref<string>("debounce");

const handleSpawn = (v:string):void=>{
    // console.log(v)
    spawnText.value = v;

    //this value controls the update animation of the spawn text
    spawnTextId.value = nanoid(5)
}

const handleSwitchFn = (v:string):void=>{
    selectedFn.value = v;
}

const goToUrl = (v:string):void=>{
    window.location.href=v;
}

const gridUrl = "http://www.zhenmingwang.online/grid-editor"
const toDoAppUrl = "http://www.zhenmingwang.online/todoApp"
</script>


<template>
<div class="body">

<div class="row">
<Card 
title="A Todo App"
width="18"
height = "10"
:onclick="()=>goToUrl(toDoAppUrl)"
>
    <div class="col card-col">
        <Image
         url="/vue.png"
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
:onclick="()=>goToUrl(gridUrl)"
>
<div class="col card-col">
    <Image
    url="/react.png"
    width="5.9"
    height="5.1"
    />
<div class="text">
    Built with React + Redux. 电脑端访问更佳
</div>
</div>
</Card>
</div>

<div class="col">
    <div class="title generic-title">
        playground
    </div>
    <div class="sub-title generic-title">
        <!-- 防抖和节流 间隔时间: 2s -->
        <ButtonGroup
        :elements="[
            {text:'防抖',value:'debounce'},
            {text:'节流',value:'throttle'}
        ]"
        defaultActive="防抖"
        v-on:switch-function="(v)=>handleSwitchFn(v)"
        />
        间隔时间: 2s
    </div>
    <div class="row" :style="{'margin-top':'1rem'}">
        <Input
        height="2"
        width="6"
        :font-size="3"
        :fn="selectedFn"
        @spawntext="handleSpawn"
        />
    </div>
    <div class="row floating-text-row" :style="{
        'border':'1px solid #F3bc21',
        'min-height':'2rem'
        }">
        <FloatingText v-bind:value="spawnText" v-bind:id="spawnTextId"/>
    </div>
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

.sub-title{
    font-size:1.1rem;
}

.floating-text-row{
    max-width:900px;
}

</style>