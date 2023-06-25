<script setup>
import { ref } from 'vue';
import { uid } from 'uid'
import CreateTodo from '../components/CreateTodo.vue';
import TodoItem from '../components/TodoItem.vue';
import { Icon } from '@iconify/vue';
const todoList = ref([]);
const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null
  })
};
// keep in mind use value on script tag when you have a reactive data and pass index as parameter to pick the todo that we are interested
const onToggleCompleted = (indexPos) => {
  todoList.value[indexPos].isCompleted = !todoList.value[indexPos].isCompleted;
};
const onEditTodo = (indexPos) => {
  todoList.value[indexPos].isEditing =!todoList.value[indexPos].isEditing;
};
const onUpdateTodo = (updatedTodo, todoPos) => {
  todoList.value[todoPos].todo = updatedTodo;
};
const onDeleteTodo = (todoPos) => {
  todoList.value.splice(todoPos, 1);
console.log(todoList.value);
}
// ----- second solution --------- 
// const onDeleteTodo = (todoId) => {
//   todoList.value = todoList.value.filter(todo => todo.id!== todoId);
// }
</script>

<template>
  <main>
    <h1>Create a Task</h1>
    <CreateTodo @create-todo="createTodo" />
    <TodoItem v-for="(todo, index) in todoList" 
    :todo="todo" 
    :index="index" 
    v-if="todoList.length > 0"
    @toggle-completed="onToggleCompleted"
    @edit-todo="onEditTodo"
    @update-todo="onUpdateTodo"
    @delete-todo="onDeleteTodo"
     
    />
    <div class="no-todo-msg" v-else>
      <Icon icon="quill:user-sad" color="#41b883" width="40" class="icon" />
      <span>You have no tasks! Please add one...</span>
    </div>
  </main>
</template>

<style lang="scss" scoped>
main {
  display: flex;
  flex-direction: column;
  max-width: 600px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }

  .no-todo-msg {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 1rem auto;
    gap: 0.5rem;

    &.icon {
      font-weight: 900;
    }
  }
}
</style>