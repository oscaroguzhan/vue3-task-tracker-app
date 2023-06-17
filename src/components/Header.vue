<script setup>
import { RouterLink } from 'vue-router';
</script>


<template>
  <header>
    <nav class="container">
      <div class="branding">
        <img src="../assets/images/ozzylogo.png" alt="brand logo">
        <h1>Task Tracker</h1>
      </div>
      <ul class="nav-routes">
        <RouterLink to="/" >Home</RouterLink>
        <RouterLink to="/about" >About</RouterLink>
      </ul>
    </nav>
  </header>
</template>


<style lang="scss" scoped>
  header {
  background-color: var(--primary-color);
  nav {
    display: flex;
    align-items: center;
    padding: 25px 16px;
    font-size: 18px;
    color:var(--white);

    .branding {
      display: flex;
      align-items: center;
      gap: 8px;
      img {
        max-width: 120px;
      }

      h1 {
        padding-left: 10px;
        font-size: 36px;
      }
    }

    .nav-routes {
      display: flex;
      flex: 1;
      justify-content: flex-end;
      gap: 12px;
      list-style: none;

      a {
        text-decoration: none;
        color: inherit;

        &:hover {
          color: var(--secondary-color);
        }
      }
    }
  }
}
</style>