<template>
<div :key="book.id" v-for="book in books">
<Book 
@toggle-update="$emit('toggle-update')"
@update-book="$emit('update-book',book.id)"
@delete-book="$emit('delete-book',book.id)" 
:book="book"/>
</div>


</template>
<script>
import Book from "./Book.vue"

export default{
    name:'Books',
    props:{
        books: Array,
    },
    components:{
        Book,
    },
    emits:['delete-book','update-book','toggle-update']

}


</script>

<style>



</style>