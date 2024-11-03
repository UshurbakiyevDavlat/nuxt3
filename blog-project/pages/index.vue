<template>
   <div>
    <h1>Blog Posts</h1>
    <div v-if="posts.length">
      <ul>
        <li v-for="post in posts" :key="post.slug" class="post-item">
          <nuxt-link :to="`/post/${post.slug}`">
            <h2>{{ post.title }}</h2>
          </nuxt-link>
          <p>By {{ post.author }} on {{ post.date }}</p>
        </li>
      </ul>
    </div>
    <div v-else>
      <p>No posts available</p>
    </div>
   </div>
</template>
  
<script setup>
import { useAsyncData } from 'nuxt/app';

const postFiles = import.meta.glob('@/data/posts.json',{eager:true});
const postsData = postFiles['/data/posts.json'].default;

const {data:posts} = useAsyncData('posts', () => postsData)
</script>

<style scoped>
h1 {
  margin-bottom: 1em;
}
.post-item {
  margin-bottom: 1em;
}
.post-item h2 {
  margin: 0;
  font-size: 1.5em;
  color: #007acc;
  cursor: pointer;
}
.post-item p {
  margin: 0.3em 0;
  color: #666
}
.post-item h2:hover {
  text-decoration: underline;
}
</style>
  