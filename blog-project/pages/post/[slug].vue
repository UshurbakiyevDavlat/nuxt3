<template>
    <div v-if="post">
        <h1>{{ post.title }}</h1>
        <p><strong>Author: </strong>{{ post.author }}</p>
        <p><strong>Date: </strong>{{ post.date }}</p>
        <div>{{ post.content }}</div>
    </div>
    <div v-else>
        <p>Post not found</p>
    </div>
</template>
  
<script setup>
import { useRoute } from 'vue-router'

const postFiles = import.meta.glob('@/data/posts.json', {eager: true});
const postsData = postFiles['/data/posts.json'].default;

const route = useRoute()
const slug = route.params.slug

const {data: post} = useAsyncData('post',() => {
    return postsData.find((post) => post.slug === slug) || null
})
</script>
  
<style>
h1 {
    margin-bottom: 0.5em
}
p {
    margin: 0.3em 0;
}
div {
    margin-top: 1em;
    line-height: 1.6;
}
</style>