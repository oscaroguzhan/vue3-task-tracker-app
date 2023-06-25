<script setup>
import { Icon } from '@iconify/vue';
const props = defineProps({
  todo: {
    type: Object,
    required: true,
  },
  index: {
    type: Number,
    required: true,
  }
});
defineEmits(['toggle-completed', 'edit-todo', 'update-todo', 'delete-todo'])
</script>

<template>
  <li>
    <input 
      type="checkbox" 
      :checked="todo.isCompleted" 
      @input="$emit('toggle-completed', index)" 
      />
    <div class="todo">
      <input 
      v-if="todo.isEditing" type="text" :value="todo.todo" @input="$emit('update-todo', $event.target.value, index)"/>
      <span v-else :class="{'completed-todo': todo.isCompleted}">{{ todo.todo }}</span>
    </div>
    <div class="todo-actions">
      <Icon v-if="todo.isEditing" icon="ph:check-circle" color="#41b883" width="28" class="icon" @click="$emit('edit-todo', index)"/>
      <Icon v-else icon="ph:pencil-fill" color="#fafafa" width="28" class="icon" @click="$emit('edit-todo', index)"/>
      <Icon icon="ic:baseline-delete" color="#f95e5e" width="28" class="icon" @click="$emit('delete-todo', todo.id)"/>
    </div>
  </li>
</template>

<style lang="scss" scoped>
li {
  margin-top: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  padding: 16px 10px;
  background-color: var(--secondary-color);
  color: #fafafa;
  &:hover {
    .todo-actions {
      opacity: 1;
    }
  }

  input[type="checkbox"] {
    appearance: none;
    width: 20px;
    height: 20px;
    background-color: #fff;
    border-radius: 50%;

    &:checked {
      background-color: var(--primary-color);
    }
  }

  .todo {
    flex: 1;
    .completed-todo {
      text-decoration: line-through;
    }
    input[type="text"] {
      width: 100%;
      padding: 6px 8px;
      border: 2px solid var(--secondary-color);
    }
  }

  .todo-actions {
    display: flex;
    gap: 6px;
    opacity: 0;
    transition: 150ms ease-in-out;

    .icon {
      cursor: pointer;
    }
  }
}
</style>