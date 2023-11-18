<script setup>
  import { ref } from "vue";
  import { Icon } from '@iconify/vue';
  import ToDocreatoe from "../components/ToDocreatoe.vue";
  import {uid} from 'uid';
   import ToDoItem from "../components/ToDoItem.vue";
 const todoList = ref([]);
 const fetchToDoList = () => {
  const savedToDoList = JSON.parse(localStorage.getItem("todoList"));
  if(savedToDoList){
    todoList.value = savedToDoList;
  }
 };

 fetchToDoList();
 const setToDoListLocalStore = () => {
  localStorage.setItem("todoList", JSON.stringify(todoList.value))
 }
 const createToDo = (todo) =>{
    todoList.value.push({
      id: uid(),
      todo,
      isCompleted: null,
      isEditing: null,
    });
    setToDoListLocalStore();
 };
 const toggleToDoComplete = (todoPos) =>{
    todoList.value[todoPos].isCompleted = ! todoList.value[todoPos].isCompleted;
    setToDoListLocalStore();
 };

 const toggleEditToDo = (todoPos) =>{
  todoList.value[todoPos].isEditing = ! todoList.value[todoPos].isEditing;
  setToDoListLocalStore();
 };

 const updatetodo = (todoVal, todoPos) => {
  todoList.value[todoPos].todo = todoVal;
  setToDoListLocalStore();
 };

 const deletetodo = (todoId) => {
    todoList.value = todoList.value.filter((todo) => todo.id !== todoId);
    setToDoListLocalStore();
 }
</script>

<template>
  <main>
    <h1 class="create-todos">Create ToDos</h1>
      <ToDocreatoe @create-todo="createToDo"/>
      <ul class="todo-list" v-if="todoList.length > 0">
        <ToDoItem v-for="(todo, index) in todoList" :todo = "todo" :index = "index" @toggle-complete="toggleToDoComplete" @edit-todo="toggleEditToDo" @update-todo="updatetodo" @delete-todo = "deletetodo"/>
      </ul>
      <p class="todos-msg" v-else>
        <Icon icon="noto-v1:sad-but-relieved-face" color="#41b080" width="22" />
        <span>You have no todo's complete</span>
      </p>
  </main>
</template>

<style scoped lang="scss">
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }
  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
}
</style>