<template>
<header>
<h1 class="text-2xl text-white">{{title}}</h1>
<Button 
@toggle-add-book="$emit('toggle-add-book')"
class="	a"
 :text="showAddBook ? 'Close' : 'Add Book'"
 :color="showAddBook ? 'red' : 'white'"
 :icon="'fas fa-plus'"
 />

  <Button 
@toggle-search-books="$emit('toggle-search-books')"
class="	a"
 :text="Searchbook ? 'Close' : 'Search Book'"
 :color="Searchbook ? 'red' : 'white'"
 :icon="'fas fa-magnifying-glass'"

 />

  <!-- <Button 
@toggle-show-books="$emit('toggle-show-books')"
class="a"
 :text="showBooks ? 'Close' : 'Show Books'"
  :color="showBooks ? 'red' : 'white'" /> -->
</header>


</template>
<script>
import Button from "./Button.vue"

export default{
    name: 'Header',
    props: {
        title: String,
        showAddBook: Boolean,
        showBooks: Boolean,
        Searchbook: Boolean,
    },
components:{
Button,
},
emits:['toggle-add-book', 'toggle-show-books' ,'toggle-search-books' ]
}

</script>
<style>

 header {
  position: relative;
    top: 0;
    left: 0;
    width: 100%;
    padding: 20px 100px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    z-index: 99;
  /* display: flex;
  justify-content: space-between; */
  /* align-items: center;
  margin-bottom: 20px; */
} 

.a {
    position: relative;
    font-size: 1.1em;
    color: white;
    text-decoration: none;
    font-weight: 50%;
    margin-left: 30px;
}

.a::after {
    content: '';
    position: absolute;
    left: 0;
    bottom: -4px;
    width: 100%;
    height: 3px;
    background: white;
    border-radius: 3px;
    transform-origin: right;
    transform: scaleZ(0);
    transition: transform .5s;
}

.a:hover::after {
    transform-origin: left;
    transform: scaleX(1);
}


</style>