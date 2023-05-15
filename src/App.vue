<script setup>
  import {ref, watch} from 'vue'

  let todos = ref(JSON.parse(window.localStorage.getItem('todos')))
  let newInput =ref('')

  watch(todos, function(value) {
    window.localStorage.setItem('todos', JSON.stringify(value))
}, {deep:true})

 function input () {
     todos.value.push({
        text: newInput.value,
        complete: false
     })
     newInput.value = ''
  }
   
function deleteItem (index) {
  todos.value.splice(index, 1)
}
   
</script>

<template>
  <h1>My todo application</h1>
  <ul>
  <li v-for="(todo, index) in todos">
    <label class="container"></label>
    <input type="checkbox" id="checked" v-model="todo.complete">
    <label for="check"></label>
    <button @click = "deleteItem (index)">💣</button>
    {{todo.text}}
  </li>
    </ul>

    <input v-model="newInput" @keydown.enter="input">
    <button @click=input>add todo</button>

  </template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Yomogi&display=swap');
body{
  font-family: 'Yomogi', cursive;
  margin: auto;
  max-width: 500px;
  background-color: #F1DEC9;
}
h1{
  color:#9F8772;
  text-decoration: underline;
  text-align: center;
}
@import url('https://fonts.googleapis.com/css2?family=Neucha&display=swap');
button{
  border-radius: 6px;
  background-color: #FFE15D;
  border-color: #B3C99C;
  border-style: dotted;
  font-family: 'Neucha';
}
input{
  border-radius: 10px;
}
input[type="checkbox"]{
  height: 20px;
  width: 20px;
  border-radius: 8px;
  cursor:pointer;
}

  

</style>
