<template>
  <div :class="theme">
    <!-- Header -->
    <header class="header">
      <div class="logo">
        <nuxt-link to="/">My Blog</nuxt-link>
      </div>
      <nav class="nav" :class="{ open: menuOpen }">
        <nuxt-link to="/">Home</nuxt-link>
        <nuxt-link to="/about">About</nuxt-link>
      </nav>
      <button class="menu-toggle" @click="toggleMenu">
        ☰
      </button>
    </header>

    <!-- Theme Toggle Button -->
    <button class="theme-toggle" @click="toggleTheme">Toggle Theme</button>

    <!-- Main Content -->
    <main>
      <NuxtPage />
    </main>

    <!-- Footer -->
    <footer class="footer">
      <p>© 2024 My Blog</p>
    </footer>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// Theme state
const theme = ref('dark')

// Menu state for responsive nav
const menuOpen = ref(false)

// Toggle the theme
function toggleTheme() {
  theme.value = theme.value === 'dark' ? 'light' : 'dark'
}

// Toggle the menu
function toggleMenu() {
  menuOpen.value = !menuOpen.value
}
</script>

<style scoped>
/* General Styles */
body {
  margin: 0;
  font-family: 'Arial', sans-serif;
}

/* Theme Styles */
.dark {
  background-color: #1e1e1e;
  color: #f5f5f5;
}

.light {
  background-color: #f5f5f5;
  color: #1e1e1e;
}

/* Header */
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1em 2em;
  background-color: inherit;
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
}

.logo {
  font-size: 1.5em;
  font-weight: bold;
}

.nav {
  display: flex;
  gap: 1.5em;
}

.nav a {
  text-decoration: none;
  color: inherit;
  font-weight: bold;
  transition: color 0.3s;
}

.nav a:hover {
  color: #007acc;
}

/* Menu Toggle (Hamburger) */
.menu-toggle {
  display: none;
  font-size: 1.5em;
  background: none;
  border: none;
  color: inherit;
  cursor: pointer;
}

.nav.open {
  display: flex;
  flex-direction: column;
  gap: 1em;
  background-color: inherit;
  padding: 1em;
  position: absolute;
  top: 100%;
  right: 0;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

/* Theme Toggle Button */
.theme-toggle {
  margin: 1em 2em;
  padding: 0.5em 1.5em;
  border: 1px solid #ccc;
  background-color: inherit;
  color: inherit;
  border-radius: 5px;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s, color 0.3s;
}

.theme-toggle:hover {
  background-color: rgba(0, 0, 0, 0.1);
}

/* Main Content */
main {
  padding: 2em;
  min-height: calc(100vh - 200px); /* Adjust for header and footer */
}

/* Footer */
.footer {
  text-align: center;
  padding: 1.5em;
  border-top: 1px solid rgba(0, 0, 0, 0.1);
  background-color: inherit;
  color: inherit;
}

/* Responsive Styles */
@media (max-width: 768px) {
  .nav {
    display: none;
  }

  .menu-toggle {
    display: block;
  }

  .nav.open {
    display: flex;
  }

  .theme-toggle {
    margin: 1em auto;
    display: block;
    text-align: center;
  }
}
</style>
