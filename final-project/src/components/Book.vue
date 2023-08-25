<template>
<div class="book m-2 p-3 bg-slate-300 ">
    <h3 class="flex items-center justify-between">{{ book.title }}
    <i  @click="onupdate(book.id)" class="text-green-600 fa-regular fa-pen-to-square cursor-pointer"></i>
    <i @click="ondelete(book.id)" class="text-red-700 fa-solid fa-trash cursor-pointer"></i>
    

    </h3>
    <p>{{ book.author }}</p>
    
</div>


</template>
<script>
export default{
    name: 'Book',
    props:{
        book: Object,
    },
    methods:{
        ondelete(id){
            this.$emit('delete-book',id)
        },
        onupdate(id){
            this.$emit('update-book',id)
            this.$emit('toggle-update')
        }
    }

}


</script>
<style>

.book{
    border-radius: 12px;
}
i{
    padding: 0;
    margin: 0;
}

/* flex items-center justify-between */
/* .book h3 {
    display: flex;
    align-items: center;
    justify-content: space-between;
  } */

</style>