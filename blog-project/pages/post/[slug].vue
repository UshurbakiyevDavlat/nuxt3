<template>
    <div>
      <h1>Blog Post</h1>
      <p>Slug: {{ slug }}</p>
    </div>
  </template>
  
  <script setup>
  import { useRoute } from 'vue-router'
  
  // Access the route parameters
  const route = useRoute()
  const slug = route.params.slug
  </script>
  