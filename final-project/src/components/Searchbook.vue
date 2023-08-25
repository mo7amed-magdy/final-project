<template>

  <div class="form-box login">
    <h2>Search</h2>
<form @submit="onSubmit">
    <div class="input-box">
      
      <input type="text" v-model="title" class="border-2 border-sky-500" name="title" placeholder="Title" />
      <label>Search By Title</label>
    </div>

    <input type="submit" value="Search" class="btn btn-block" />
  </form>


  </div>



</template>

<script>
export default{
    name: 'Searchbook',
    data(){
        return{
            title: '',
        }

    },
    methods: {
    onSubmit(e) {
      e.preventDefault()

      if (!this.title) {
        alert('Please add an id')
        return
      }

      const sBook = {
        title: this.title,
        
      }
       console.log(sBook);
      this.$emit('search-book', sBook)

      this.title = ''
    },
  },
}



</script>

<style>

.add-form {
  margin-bottom: 40px;
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

.input-box {
    position: relative;
    width: 100%;
    height: 50px;
    border-bottom: 2px solid black;
    margin: 30px 0;
}

.input-box label {
    position: absolute;
    top: 55%;
    left: 5px;
    transform: translateY(-50%);
    font-size: 1em;
    color: white;
    font-weight: 500;
    pointer-events: none;
    transition: .5s;
}

.input-box input:focus~label,
.input-box input:valid~label {
    top: -7px;
}

.input-box input {
    width: 100%;
    height: 100%;
    background: transparent;
    border: none;
    outline: none;
    font-size: 1em;
    color: white;
    font-weight: 600;
}
.form-box.login {
    transition: transfrom .18s ease;
    transform: translateX(0);
}
.form-box h2 {
    font-size: 2em;
    color: white;
    text-align: center;
}


</style>