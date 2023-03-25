<template>
  <nav class="filternav">
    <button @click="filterBy('all')" :class="{active:current=='all'}">view all</button>
    <button @click="filterBy('complete')" :class="{active:current=='complete'}">complete</button>
    <button @click="filterBy('ongoing')" :class="{active:current=='ongoing'}">ongoing</button>
  </nav>
</template>

<script>
export default {
    props:['current'],
    methods:{
        filterBy(value){
        this.$emit("firstValue",value)
    }
    }

}
</script>

<style>
.filternav button{
    background: none;
    border:none;
    outline:none;
    color: #bbb;
    font-size:12px;
    font-weight: bold;
    text-transform: uppercase;
    cursor: pointer;
    margin-right: 10px;
    letter-spacing: 1px;
}

button.active{
    color:#333;
    border-bottom: 2px solid #00ce89;
    padding-bottom: 4px;
}
</style>