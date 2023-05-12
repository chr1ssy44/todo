<script setup>
  import {ref} from 'vue'

  let todos = ref([])
  let newInput =ref('')

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
    <input type="checkbox" v-model="todo.complete">
    <button @click = "deleteItem (index)">💣</button>
    {{todo.text}}
    {{index}}
  </li>
    </ul>

    <input v-model="newInput" @keydown.enter="input">
    <button @click=input>add todo</button>

  </template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Vibes&display=swap');
body{
  font-family: 'Vibes', cursive;
  margin: auto;
  max-width: 500px;
  background-color: #FDEFEF;
}
h1{
  color:#9F8772;
  text-decoration: underline;
  text-align: center;
}
button{
  border-radius: 6px;
  background-color: #FFE15D;
}
input{
  border-radius: 10px;
}
</style>
