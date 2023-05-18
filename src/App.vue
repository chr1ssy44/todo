<script setup>
  import {ref, watch} from 'vue'

  let todos = ref(JSON.parse(window.localStorage.getItem('todos')) ?? [])
  let newInput = ref('')

  let filter = ref('all')

  watch(todos, function(value) {
    window.localStorage.setItem('todos', JSON.stringify(value))
}, {deep:true})

 function input () {
     todos.value.push({text: newInput.value,complete: false})
     newInput.value = ''
  }
   
function deleteItem (index) {
  todos.value.splice(index, 1)
}

function todoFilter (todo) {
  if (filter.value == 'active') {
    return todo.complete == false
  } else {
    return true
  }
}
  
  function activeFilter (todo) {
    return todo.complete ==false
  }
</script>

<template>
  <h1>My todo application</h1>

<p v-if="todos.length > 0">
  <input name="filter" type="radio" value="all" v-model="filter">
  <label>all</label>

  <input name="filter" type="radio" value="active" v-model="filter">
  <label>active</label>

  <input  name="filter" type="radio" value="complete" v-model="filter">
  <label>complete</label>
</p>

 <p>
  {{ todos.filter(activeFilter).length }} items left
</p>

  <ul>
  <li v-for="(todo, index) in todos.filter(todoFilter)" :class="{completed: todo.complete}">
<div class="checkbox">
  <input :id="'check' + index" type="checkbox" v-model="todo.complete">
  <label id="lab" :for="'check' + index"></label>
</div>
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
  margin: 15px 2px ;

}
input{
  border-radius: 10px;
  padding: 25px;
  border-style: outset;
  border-color: #B3C99C;
  font-size: medium;
}
#lab {
  display: inline-block;
  cursor: pointer;
  position: relative;
  padding-left: 25px;
  margin-right: 15px;
  font-size: 11px;
}
#lab:before {
  content: "";
  display: inline-block;
  width: 18px;
  height: 18px;
  margin-right: 10px;
  position: absolute;
  left: 0;
  bottom: 1px;
  background-color:white;
  box-shadow: inset 0px 2px 3px 0px rgba(0, 0, 0, .3), 0px 1px 0px 0px rgba(255, 255, 255, .8);
}

input[type=checkbox] {
  display: none;
}
.checkbox #lab:before {
  border-radius: 15px;
}
input[type=checkbox]:checked + #lab:before {
  content: "\2713";
  font-size: 12px;
  color: rgb(63, 190, 21);
  text-align: center;
  line-height: 25px;
}

.completed{
  text-decoration: line-through;
  color: green;
}
</style>
