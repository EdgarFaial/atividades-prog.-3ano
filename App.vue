<script setup lang="ts">
import { ref } from "vue"

interface Todo {
  id: number
  text: string
  done: boolean
}

interface TodoList {
  id: number
  title: string
  newTask: string
  todos: Todo[]
}

let listId = 1
let todoId = 1

const newList = ref("")

const lists = ref<TodoList[]>([
  {
    id: listId++,
    title: "Faculdade",
    newTask: "",
    todos: [
      {
        id: todoId++,
        text: "Estudar Vue",
        done: false
      }
    ]
  }
])

function addList() {
  if (!newList.value.trim()) return

  lists.value.push({
    id: listId++,
    title: newList.value,
    newTask: "",
    todos: []
  })

  newList.value = ""
}

function removeList(id:number){
  lists.value = lists.value.filter(l => l.id != id)
}

function addTask(list:TodoList){

  if(!list.newTask.trim()) return

  list.todos.push({
    id: todoId++,
    text: list.newTask,
    done:false
  })

  list.newTask=""
}

function removeTask(list:TodoList,id:number){
  list.todos = list.todos.filter(t => t.id != id)
}
</script>

<template>

<div class="container">

<h1>📝 Gerenciador de Tarefas</h1>

<div class="nova-lista">

<input
v-model="newList"
placeholder="Nome da lista"
/>

<button @click="addList">
Criar Lista
</button>

</div>

<div class="listas">

<div
class="lista"
v-for="lista in lists"
:key="lista.id"
>

<div class="cabecalho">

<h2>{{ lista.title }}</h2>

<button
class="removerLista"
@click="removeList(lista.id)"
>
✖
</button>

</div>

<div class="novaTarefa">

<input
v-model="lista.newTask"
placeholder="Nova tarefa"
/>

<button @click="addTask(lista)">
Adicionar
</button>

</div>

<ul>

<li
v-for="todo in lista.todos"
:key="todo.id"
>

<label>

<input
type="checkbox"
v-model="todo.done"
/>

<span
:class="{done:todo.done}"
>
{{todo.text}}
</span>

</label>

<button
class="delete"
@click="removeTask(lista,todo.id)"
>
🗑
</button>

</li>

</ul>

</div>

</div>

</div>

</template>

<style scoped>

*{
font-family:Arial, Helvetica, sans-serif;
}

body{
background:#f4f6f9;
}

.container{
max-width:1100px;
margin:auto;
padding:30px;
}

h1{
text-align:center;
margin-bottom:30px;
color:#34495e;
}

.nova-lista{
display:flex;
gap:10px;
margin-bottom:30px;
}

input{

padding:10px;
border-radius:8px;
border:1px solid #ccc;
flex:1;

}

button{

padding:10px 18px;
border:none;
border-radius:8px;
background:#42b883;
color:white;
cursor:pointer;
transition:.2s;

}

button:hover{
background:#369b6d;
}

.listas{

display:grid;
grid-template-columns:repeat(auto-fit,minmax(320px,1fr));
gap:20px;

}

.lista{

background:white;
padding:20px;
border-radius:15px;
box-shadow:0 5px 15px rgba(0,0,0,.1);

}

.cabecalho{

display:flex;
justify-content:space-between;
align-items:center;

}

.removerLista{
background:#e74c3c;
}

.removerLista:hover{
background:#c0392b;
}

.novaTarefa{

display:flex;
gap:10px;
margin:20px 0;

}

ul{

list-style:none;
padding:0;

}

li{

display:flex;
justify-content:space-between;
align-items:center;
padding:8px 0;

}

.done{

text-decoration:line-through;
color:gray;

}

.delete{
background:#555;
}

.delete:hover{
background:black;
}

</style>