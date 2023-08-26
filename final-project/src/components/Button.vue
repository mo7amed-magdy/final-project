<template>

<button :style="{color: color}" @click="onclick()" >{{text}}
<i :class="icon"
></i>
</button>

</template>

<script>
export default{
name:'Button',
props:{
    text: String,
    color: String,
    icon:String
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