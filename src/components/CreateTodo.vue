  <script setup>
  import { reactive } from 'vue';
  import TodoButton from '../components/TodoButton.vue'
  const todo = reactive({
    todo: "",
    isInvalid:null,
    errMsg:false
  })
  const emit = defineEmits(['create-todo'])
  
  // define the function that will will listen by parent component when we emit
  const createTodo = () => {
    todo.isInvalid = null;
    if(todo.todo !== '') {
      emit('create-todo', todo.todo)
      todo.todo = ''
      return;
    }
    todo.isInvalid = true;
    todo.errMsg = 'Please write a todo...';
  };
  </script>

<template>
  <!-- dynamic styling with certain condition -->
  <div class="input-wrap" :class="{'input-err' : todo.isInvalid}">
    <input type="text" v-model="todo.todo">
    <!-- when we click event on child component and want to listen on parent component use emit -->
    <TodoButton @click="createTodo()">Create </TodoButton>
  </div>
  <p v-show="todo.isInvalid" class="err">{{ todo.errMsg }}</p>
</template>


<style lang="scss" scoped>
.input-wrap {
  display: flex;
  transition: 250ms ease;
  border: 2px solid var(--secondary-color);

  &:focus-within {
    box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
      0 -2px 4px -2px rgb(0 0 0 / 0.1);
  }
  &.input-err {
    border: 2px solid red;
  }
  input {
    width: 100%;
    padding: 10px 8px;
    border: none;

    &:focus {
      outline: none;
    }
  }
  
}
.err {
  color: red;
  text-align: center;
  margin-top: 6px;
  font-size: 18px;
}
</style>