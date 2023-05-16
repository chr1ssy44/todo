<script setup>
  import {ref, watch} from 'vue'

  let todos = ref(JSON.parse(window.localStorage.getItem('todos')) ?? [])
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
  <li v-for="(todo) in todos" :class="{completed: todo.complete}">
    <label class="container"></label>
    <input type="checkbox" id="checked" v-model="todo.complete">
    <label for="check"></label>
    <button @click = "deleteItem" id="bomb">❌</button>
    {{todo.text}}
  </li>
    </ul>

    <input v-model="newInput" @keydown.enter="input">
    <button @click=input id="add">add todo</button>

  </template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Englebert&display=swap');
body{
  font-family: 'Englebert', sans-serif;
  display: flex;
  justify-content: center;
  background-color: #F1DEC9;
  margin: 300px;
}
h1{
  color:#9F8772;
  text-decoration: underline;
}
@import url('https://fonts.googleapis.com/css2?family=Neucha&display=swap');
#add{
  border-radius: 50%;
  background-color: #FFE15D;
  border-color: #B3C99C;
  border-style: outset;
  font-family: 'Neucha';
  cursor: pointer;
  padding: 25px;
  box-shadow: 0 9px #999;
}
#add:active{
  background-color: #B3C99C;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
}
#bomb{
  border-radius: 50%;
  background-color: #FFE15D;
  border-color: #B3C99C;
  border-style: dotted;
  font-family: 'Neucha';
  cursor: pointer;
  padding: 10px;
}
input{
  border-radius: 10px;
  padding: 25px;
  border-style: outset;
  border-color: #B3C99C;
  font-size: medium;
  
}
input[type="checkbox"]{
  height: 20px;
  width: 20px;
  border-radius: 8px;
  cursor:pointer;
}
.completed{
  text-decoration: line-through;
  color: #5D9C59;
}

</style>
