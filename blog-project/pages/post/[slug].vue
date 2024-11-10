<template>
    <div class="post-page" :class="theme">
      <h1 class="post-title">{{ post.title }}</h1>
      <div class="post-meta" :class="theme">
        <p><strong>Author:</strong> {{ post.author }}</p>
        <p><strong>Date:</strong> {{ post.date }}</p>
      </div>
      <div class="post-content" :class="theme">
        <p v-for="(paragraph, index) in formattedContent" :key="index">{{ paragraph }}</p>
      </div>
      <button class="back-button" :class="theme" @click="goBack">Back to Homepage</button>
    </div>
  </template>
  
  <script setup>
  import { useRoute, useRouter } from 'vue-router'
  
  // Reactive theme (inherits from app-level state if possible)
  const theme = inject('theme')
  
  // Import posts data
  const postFiles = import.meta.glob('@/data/posts.json', { eager: true })
  const postsData = postFiles['/data/posts.json'].default
  
  // Get the current slug
  const route = useRoute()
  const router = useRouter()
  const slug = route.params.slug
  
  // Find the post matching the slug
  const post = postsData.find((p) => p.slug === slug)
  // Format the content into paragraphs (if the content is a single string)
  const formattedContent = post ? post.content.split('\n\n') : []
  
  // Go back to the homepage
  function goBack() {
    router.push('/')
  }
  </script>
  
  <style scoped>
  /* Post Page Styling */
  .post-page {
    max-width: 800px;
    margin: 0 auto;
    padding: 2em;
    background-color: white;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 8px;
    transition: background-color 0.3s, color 0.3s; /* Smooth theme transition */
  }
  
  .post-page.dark {
    background-color: #1e1e1e; /* Dark background */
    color: #e0e0e0; /* Light text */
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.5); /* Softer shadow */
  }
  
  /* Post Title */
  .post-title {
    font-size: 2.5em;
    margin-bottom: 0.5em;
    color: #007acc;
    text-align: center;
  }
  
  .post-title.dark {
    color: #60a5fa; /* Lighter blue in dark mode */
  }
  
  /* Meta Information */
  .post-meta {
    margin-bottom: 1.5em;
    color: #666;
    text-align: center;
  }
  
  .post-meta.dark {
    color: #aaa; /* Softer gray in dark mode */
  }
  
  /* Post Content */
  .post-content p {
    margin-bottom: 1.2em;
    line-height: 1.8;
    font-size: 1.2em;
    color: #333;
  }
  
  .post-content.dark p {
    color: #ddd; /* Light gray for dark mode */
  }
  
  /* Back Button */
  .back-button {
    display: block;
    margin: 2em auto;
    padding: 0.8em 2em;
    background-color: #007acc;
    color: white;
    font-size: 1em;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .back-button:hover {
    background-color: #005f99;
  }
  
  .back-button.dark {
    background-color: #60a5fa; /* Light blue in dark mode */
    color: #1e1e1e; /* Dark text for contrast */
  }
  
  .back-button.dark:hover {
    background-color: #3b82f6;
  }
  </style>
  