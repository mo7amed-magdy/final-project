<template>
    <form @submit="onSubmit" class="add-form">

        <div class="form-control">
          <label>New Title</label>
          <input type="text" v-model="newtitle" class="border-2 border-sky-500" name="newtitle" placeholder="Add Title" />
        </div>

        <div class="form-control">
          <label> New Author</label>
          <input type="text" v-model="newauthor" class="border-2 border-sky-500" name="newauthor" placeholder="new Author" />
        </div>

        <input type="submit" value="Update" class="btn btn-block" />
  </form>
  </template>

<script>


export default{
    name:'Update',
    data(){
        return{
            newtitle: '',
            newauthor: '',
            
        }

    },
    
    methods: {
    onSubmit(e) {
      e.preventDefault()

      if (!this.newtitle) {
        alert('Please add a title')
        return
      }

      const uBook = {
        title: this.newtitle,
        author: this.newauthor,
      }
      console.log(uBook);
      this.$emit('add-book', uBook)

      this.newtitle = ''
      this.newauthor = ''
    },
  },
}



</script>

<style>
.add-form {
  margin-bottom: 40px;
}
label{
  color: white;
}

.form-control {
  margin: 20px 0;
}

.form-control label {
  display: block;
}

.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn-block {
  display: block;
  width: 100%;
}


</style>