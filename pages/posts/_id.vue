<template>
  <section class="container">
    <h1>{{post.title}}</h1>
    <p>{{post.body}}</p>
  </section>
</template>

<script>
  import axios from 'axios'
  export default {
    data() {
      return {
        id: this.$route.params.id,
        post: {}
      }
    },
    mounted() {
      axios.get(`https://jsonplaceholder.typicode.com/posts/${this.id}`)
        .then(response => {
          this.post = response.data
        })
    }
  }
</script>
