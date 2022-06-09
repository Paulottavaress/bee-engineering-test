<script setup>
  import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="logo-container">
      <img src="/public/images/logo.png" alt="DataHow logo">
    </div>
    <nav>
      <RouterLink class="nav-link" to="/">Home</RouterLink>
      <RouterLink class="nav-link" to="/about">About</RouterLink>
    </nav>
  </header>
</template>
<style lang="scss" scoped>
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;

    .logo-container {
      width: 200px;
      height: 100px;
      display: flex;
      justify-content: center;
      align-items: center;

      img {
        width: 100%;
        height: auto;
      }
    }
  }

  @media (max-width: 768px) {
    header {
      flex-direction: column;
    }
  }
</style>

<style lang="scss">
  header {
    nav {
      display: flex;
      gap: 5px;

      .nav-link {
        display: inline-block;
        padding: 5px;
        color: #FF2600;
        border: 1px solid #333;
        border-radius: 5px;
        text-decoration: none;
      }

      .nav-link:hover {
        background: #333;
      }
    }
  }
</style>