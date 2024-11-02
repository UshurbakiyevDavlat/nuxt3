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
/* Global theme styles */
.dark {
  background-color: #333;
  color: white;
}

.light {
  background-color: #f9f9f9;
  color: #333;
}

/* Header and Navigation */
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1em;
  background-color: inherit;
  color: inherit;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

nav {
  display: flex;
  gap: 1em;
}

nav a {
  color: inherit;
  text-decoration: none;
  font-weight: bold;
  transition: color 0.3s;
}

nav a:hover {
  color: #007acc;
}

/* Theme Toggle Button */
button {
  padding: 0.5em 1em;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-weight: bold;
  background-color: inherit;
  color: inherit;
  transition: background-color 0.3s, color 0.3s;
}

button:hover {
  background-color: rgba(0, 0, 0, 0.1);
}

/* Main Content Styling */
main {
  padding: 2em;
  min-height: calc(100vh - 160px); /* Adjust to make room for header and fixed footer */
  box-sizing: border-box;
}

/* Footer */
footer {
  padding: 1em;
  text-align: center;
  background-color: inherit;
  color: inherit;
  box-shadow: 0 -2px 5px rgba(0, 0, 0, 0.1);
  position: fixed;
  bottom: 0;
  width: 100%;
}

/* Responsive Adjustments */
@media (max-width: 600px) {
  header, footer {
    flex-direction: column;
    padding: 1em 0.5em;
    text-align: center;
  }

  nav {
    flex-direction: column;
    gap: 0.5em;
  }

  button {
    margin-top: 0.5em;
  }
}
</style>

