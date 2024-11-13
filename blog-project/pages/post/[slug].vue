<template>
    <div class="post-page" :class="theme">
      <div v-if="pending">Loading...</div>
      <div v-else-if="postData">
        <h1 class="post-title">{{ postData.title }}</h1>
        <div class="post-meta">
          <p><strong>Author:</strong> {{ postData.author }}</p>
          <p><strong>Date:</strong> {{ postData.date }}</p>
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
      <div v-else-if="error">Failed to load post: {{ error.message }}</div>
      <div v-else>
        <p>Post not found.</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { inject, ref, watchEffect } from 'vue'
  import { useRoute } from 'vue-router'
  
  // Inject the theme
  const { theme } = inject('theme')
  
  // Route and post data
  const route = useRoute()
  const slug = route.params.slug
  
  // Fetch the post by slug
  const { data: post, pending, error } = useFetch(`http://localhost:3001/posts?slug=${slug}`)
  const postData = ref(null)
  const formattedContent = ref([])
  
  // Watch for data updates
  watchEffect(() => {
    if (post.value && post.value.length) {
      postData.value = post.value[0]
      formattedContent.value = postData.value.content.split('\n\n')
    }
  })
  
  // Like button state
  const isLiked = ref(false)
  const likes = ref(0)
  
  // Load likes from localStorage
  watchEffect(() => {
    if (postData.value && process.client) {
      const savedLikes = localStorage.getItem(`likes-${postData.value.slug}`)
      likes.value = savedLikes ? parseInt(savedLikes, 10) : 0
    }
  })
  
  // Toggle like
  function toggleLike() {
    isLiked.value = !isLiked.value
    likes.value += isLiked.value ? 1 : -1
    if (postData.value) {
      localStorage.setItem(`likes-${postData.value.slug}`, likes.value)
    }
  }
  
  // Back to homepage
  function goBack() {
    window.history.back()
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
  