<template>
  <section class="container">
    <h1>Gorilla News Posts</h1>
    <div>
      <ul v-for="post in posts" :key="post.id">
        <li>{{ post }}</li>
      </ul>
    </div>
  </section>
</template>

<script>
  export default {
    async asyncData({ app }) {
      const posts = await app.$axios.$get('/api/')
      return { posts }
    }
  }
</script>
