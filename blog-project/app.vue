<template>
  <div :class="theme">
    <header>
      <nav>
        <nuxt-link to="/">Home</nuxt-link>
        <nuxt-link to="/about">About</nuxt-link>
      </nav>
      <button @click="toggleTheme">Toggle Theme</button>
    </header>

    <main>
      <NuxtPage />
    </main>

    <footer :class="theme">
      <p>© 2024 My Blog</p>
    </footer>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const theme = ref('dark')

function toggleTheme() {
  theme.value = theme.value === 'dark' ? 'light' : 'dark'
}
</script>

<style>
/* Global styles */
.dark {
  background-color: #333;
  color: white;
}

.light {
  background-color: #fff;
  color: black;
}

header, footer {
  padding: 1em;
  text-align: center;
}

footer {
  position: fixed;
  bottom: 0;
  width: 100%;
}
</style>
