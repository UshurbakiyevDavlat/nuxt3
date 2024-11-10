<template>
    <div class="post-page" :class="theme">
      <h1 class="post-title">{{ post.title }}</h1>
      <div class="post-meta">
        <p><strong>Author:</strong> {{ post.author }}</p>
        <p><strong>Date:</strong> {{ post.date }}</p>
      </div>
      <div class="post-content">
        <p v-for="(paragraph, index) in formattedContent" :key="index">{{ paragraph }}</p>
      </div>
  
      <!-- Like Button -->
      <button class="like-button" @click="toggleLike">
        {{ isLiked ? 'Unlike' : 'Like' }} ({{ likes }})
      </button>
  
      <button class="back-button" @click="goBack">Back to Homepage</button>
    </div>
  </template>
  
  <script setup>
  import { inject, ref } from 'vue'
  import { useRoute, useRouter } from 'vue-router'
  
  // Inject the theme
  const { theme } = inject('theme')
  
  // Route and post data
  const route = useRoute()
  const router = useRouter()
  const postFiles = import.meta.glob('@/data/posts.json', { eager: true })
  const postsData = postFiles['/data/posts.json'].default
  const slug = route.params.slug
  const post = postsData.find((p) => p.slug === slug)
  const formattedContent = post ? post.content.split('\n\n') : []
  
  // Like button state
  const isLiked = ref(false)
  const likes = ref(0)
  
  // Load likes from localStorage
  if (post) {
    const savedLikes = localStorage.getItem(`likes-${post.slug}`)
    likes.value = savedLikes ? parseInt(savedLikes, 10) : 0
  }
  
  // Toggle like
  function toggleLike() {
    isLiked.value = !isLiked.value
    likes.value += isLiked.value ? 1 : -1
    if (post) {
      localStorage.setItem(`likes-${post.slug}`, likes.value)
    }
  }
  
  // Back to homepage
  function goBack() {
    router.push('/')
  }
  </script>
  
  <style scoped>
  /* Like Button Styling */
  .like-button {
    display: block;
    margin: 1.5em auto;
    padding: 0.8em 1.5em;
    font-size: 1em;
    color: white;
    background-color: #007acc;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .like-button:hover {
    background-color: #005f99;
  }
  
  .back-button {
    margin: 1em auto;
    display: block;
    padding: 0.8em 1.5em;
    background-color: #333;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .back-button:hover {
    background-color: #555;
  }
  </style>
  