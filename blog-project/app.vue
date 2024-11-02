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
/* Theme styles to set background and text color based on the selected theme */
.dark {
  background-color: #333; /* Dark gray background for dark theme */
  color: white; /* White text for dark theme */
}

.light {
  background-color: #f9f9f9; /* Light background for light theme */
  color: #333; /* Dark text for light theme */
}

/* Header and Navigation styling */
header {
  display: flex; /* Flex layout for horizontal alignment */
  justify-content: space-between; /* Space between nav links and button */
  align-items: center; /* Center items vertically */
  padding: 1em; /* Padding around header */
  background-color: inherit; /* Inherit background from theme */
  color: inherit; /* Inherit text color from theme */
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1); /* Subtle shadow for depth */
}

/* Navigation links container */
nav {
  display: flex; /* Horizontal alignment for links */
  gap: 1em; /* Space between each link */
}

/* Styling for individual navigation links */
nav a {
  color: inherit; /* Inherit color based on theme */
  text-decoration: none; /* Remove underline */
  font-weight: bold; /* Bold text for emphasis */
  transition: color 0.3s; /* Smooth color change on hover */
}

/* Hover effect for navigation links */
nav a:hover {
  color: #007acc; /* Change to blue on hover */
}

/* Theme toggle button styling */
button {
  padding: 0.5em 1em; /* Padding for clickable area */
  border: none; /* Remove default border */
  border-radius: 5px; /* Rounded corners for a modern look */
  cursor: pointer; /* Pointer cursor on hover */
  font-weight: bold; /* Bold font for readability */
  background-color: inherit; /* Inherit background color from theme */
  color: inherit; /* Inherit text color from theme */
  transition: background-color 0.3s, color 0.3s; /* Smooth hover effect */
}

/* Hover effect for the toggle button */
button:hover {
  background-color: rgba(0, 0, 0, 0.1); /* Light shade on hover */
}

/* Main content styling */
main {
  padding: 2em; /* Padding for spacing */
  min-height: calc(100vh - 160px); /* Ensure main content fills available space */
  box-sizing: border-box; /* Include padding in width and height calculations */
}

/* Footer styling */
footer {
  padding: 1em; /* Padding for spacing */
  text-align: center; /* Center-align footer text */
  background-color: inherit; /* Inherit background color from theme */
  color: inherit; /* Inherit text color from theme */
  box-shadow: 0 -2px 5px rgba(0, 0, 0, 0.1); /* Subtle shadow for depth */
  position: fixed; /* Fix footer at the bottom */
  bottom: 0; /* Align to the bottom of the viewport */
  width: 100%; /* Full width to span across the screen */
}

/* Responsive adjustments for small screens */
@media (max-width: 600px) {
  /* Stack header and footer elements vertically on small screens */
  header, footer {
    flex-direction: column; /* Vertical alignment */
    padding: 1em 0.5em; /* Adjust padding */
    text-align: center; /* Center-align text */
  }

  /* Stack navigation links vertically on small screens */
  nav {
    flex-direction: column; /* Vertical alignment */
    gap: 0.5em; /* Reduced gap for spacing */
  }

  /* Add margin to separate button from nav links */
  button {
    margin-top: 0.5em; /* Add space above button */
  }
}
</style>
