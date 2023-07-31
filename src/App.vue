<script setup>
import { ref } from 'vue'

const newTodo = ref('');
const todos = ref([
  {
    id: 1,
    task: "Example Task",
    done: false,
  }
])

const showCompleted = ref(true);

function addTodo() {
  let id = Math.max(0, ...todos.value.map(todo => todo.id)) + 1
  todos.value.push({ id: id, task: newTodo.value, done: false})
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter(t => t !== todo);
}

function viewCompletedTodos() {
  showCompleted.value = !showCompleted.value
} 


function checkboxClicked(todo) {
  const foundTodo = todos.value.find(t => t === todo);
}

</script>


<template>
  <div id="app">
    <h1>Vue Todos</h1>
    <div class="inputDiv">
      <input v-model="newTodo" />
      <button @click="addTodo">Add</button>
    </div>


<div class="remaining">
  <h3>Tasks Remaining</h3>
      <ul class="todoDiv">
        <li v-for="todo in todos.filter(todo => !todo.done)" :key="todo.id">
          <input type="checkbox" v-model="todo.done" @click="checkboxClicked(todo)"/>
          <h4>Task {{ todo.id }}: {{ todo.task }}</h4>
          <button @click="removeTodo(todo)">X</button>
        </li>
      </ul>
</div>

  
    <button @click="viewCompletedTodos" v-if="showCompleted">Hide Completed</button>
    <button @click="viewCompletedTodos" v-else>Show Completed</button>
  
<div class="completed" v-if="showCompleted"><h3>Completed Tasks</h3>
  <ul class="todoDiv">
        <li v-for="todo in todos.filter(todo => todo.done)" :key="todo.id">
          <input type="checkbox" v-model="todo.done" @click="checkboxClicked(todo)"/>
          <h4>Task {{ todo.id }}: {{ todo.task }}</h4>
          <button @click="removeTodo(todo)" class="delete">X</button>
        </li>
      </ul>
</div>
  
  </div>
</template>


<style scoped>
#app {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 1em;
}

.inputDiv {
  display: flex;
  gap: 0.5em;
}

.todoDiv {
  display: flex;
  flex-direction: column;
  justify-content: center;
}


li button {
  background: red;
  border: none;
  color: #eee;
  border-radius: 3px;
  padding: 3px;

}
li {
  display: flex;
  gap: 0.5em;
  list-style-type: none;
}
</style>