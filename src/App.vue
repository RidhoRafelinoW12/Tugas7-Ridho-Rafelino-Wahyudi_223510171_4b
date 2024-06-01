<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div class="app-background">
    <header>
      <div class="wrapper">
        <HelloWorld msg="Tugas 7 Praktikum PBK!" />
        <nav>
          <RouterLink to="/about">Lets Goooo</RouterLink>
        </nav>
      </div>
    </header>
    <RouterView />
  </div>
</template>

<style scoped>
.app-background {
  background: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url('@/assets/pp1.jpeg') no-repeat center center;
  background-size: cover;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: white;
  font-family: Arial, sans-serif;
}

header {
  width: 100%;
  padding: 20px;
  background: rgba(0, 0, 0, 0.5);
}

.wrapper {
  max-width: 1200px;
  margin: 0 auto;
  text-align: center;
}

nav {
  margin-top: 10px;
}

nav a {
  color: white;
  margin: 0 15px;
  text-decoration: none;
  font-weight: bold;
}

nav a:hover {
  text-decoration: underline;
}
</style>
