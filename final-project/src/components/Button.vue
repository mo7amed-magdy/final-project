<template>

<button :style="{color: color}" @click="onclick()" >{{text}}</button>

</template>

<script>
export default{
name:'Button',
props:{
    text: String,
    color: String
},
methods:{
    onclick(){
    this.$emit('toggle-add-book')
    this.$emit('toggle-show-books')
    this.$emit('toggle-search-books')
    
    },
}
}

</script>

<style>



</style>