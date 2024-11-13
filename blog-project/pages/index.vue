<template>
  <div>
    <h1>Blog Posts</h1>
    
    <input
      v-model="searchTerm"
      type="text"
      placeholder="Search posts..."
      class="search-input"
    />

    <div v-if="paginatedPosts.length">
      <ul>
        <li v-for="post in paginatedPosts" :key="post.slug" class="post-item">
          <nuxt-link :to="`/post/${post.slug}`">
            <h2>{{ post.title }}</h2>
          </nuxt-link>
          <p>By {{ post.author }} on {{ post.date }}</p>
        </li>
      </ul>
    </div>

    <div v-else-if="error">Failed to load post: {{ error.message }}</div>

    <div v-else>
      <p>No posts found.</p>
    </div>

    <!-- Pagination Controls -->
    <div class="pagination">
      <button :disabled="currentPage === 1" @click="prevPage">Previous</button>
      <span>Page {{ currentPage }} of {{ totalPages }}</span>
      <button :disabled="currentPage === totalPages" @click="nextPage">Next</button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// Reactive search term
const searchTerm = ref('')

// Fetch posts from the mock API
const { data: posts, error } = useFetch('http://localhost:3001/posts')

// Pagination state
const postsPerPage = 5
const currentPage = ref(1)

// Computed property for filtered posts
const filteredPosts = computed(() => {
  return posts.value?.filter((post) =>
    post.title.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
    post.content.toLowerCase().includes(searchTerm.value.toLowerCase())
  )
})

// Computed property for paginated posts
const paginatedPosts = computed(() => {
  const start = (currentPage.value - 1) * postsPerPage
  const end = start + postsPerPage
  return filteredPosts.value.slice(start, end)
})

// Total pages
const totalPages = computed(() => Math.ceil(filteredPosts.value.length / postsPerPage))

// Methods to change pages
function nextPage() {
  if (currentPage.value < totalPages.value) {
    currentPage.value++
  }
}

function prevPage() {
  if (currentPage.value > 1) {
    currentPage.value--
  }
}
</script>

<style scoped>
h1 {
  margin-bottom: 1em;
}

.search-input {
  margin-bottom: 1em;
  padding: 0.5em;
  width: 100%;
  max-width: 400px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 1em;
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
  color: #666;
}

.post-item h2:hover {
  text-decoration: underline;
}

.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1em;
  margin-top: 1.5em;
}

.pagination button {
  padding: 0.5em 1em;
  font-size: 1em;
  border: 1px solid #ccc;
  background-color: white;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.pagination button:hover {
  background-color: #f0f0f0;
}

.pagination button:disabled {
  background-color: #ddd;
  cursor: not-allowed;
}

.pagination span {
  font-size: 1em;
  font-weight: bold;
}
</style>
