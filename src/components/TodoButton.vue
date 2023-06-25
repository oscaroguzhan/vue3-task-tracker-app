<script setup>

</script>

<template>
  <button @click="createTodo">
  <slot></slot>
  </button>
</template>

<style lang="scss" scoped>
button {
    padding: 8px 20px;
    border: none;
    background-color: var(--secondary-color);
    color: var(--white);
    font-size: 16px;
  }
</style>