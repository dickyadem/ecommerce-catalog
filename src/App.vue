<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'

</script>

<template>
  <header>
    <nav>
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/ManView">Clothing Man</RouterLink>
      <RouterLink to="/WomanView">Clothing Woman</RouterLink>
    </nav>
  </header>

  <RouterView />
</template>

<style scoped>
body {
  margin: 0;
  padding: 0;
  background-color: aliceblue;
}
header {
  line-height: 1.5;
  max-height: 10vh;
}

nav {
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 1;
  
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }


  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
