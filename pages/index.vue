<template>
  <section class="container">
    <table class="table">
      <thead>
      <tr>
        <th>ID</th>
        <th>Title</th>
        <th>Body</th>
        <td>Actions</td>
      </tr>
      </thead>
      <tbody>
      <tr v-for="post in posts"
          >
        <td>{{post.id}}</td>
        <td>{{post.title}}</td>
        <td>{{post.body}}</td>
        <td>
          <nuxt-link
            :to="{name: 'posts-id', params: {id: post.id}}"
            :key="post.id">
            View
          </nuxt-link>
        </td>
      </tr>
      </tbody>
    </table>
  </section>
</template>

<script>
  import axios from 'axios'

  export default {
    data() {
      return {
        posts: []
      }
    },
    mounted() {
      axios.get('https://jsonplaceholder.typicode.com/posts')
        .then(response => {
          this.posts = response.data
        })
    }
  }
</script>

