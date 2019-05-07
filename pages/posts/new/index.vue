<template>
  <section class="container">
    <h1>{{post.title}}</h1>

    <form @submit.prevent="submit()">
      <div class="form-group">
        <label for="title">Title</label>
        <input type="text"
               class="form-control"
               id="title"
               :placeholder="post.title"
               v-model="post.title">
      </div>

      <div class="form-group">
        <label for="body">Content</label>
        <textarea class="form-control"
                  id="body"
                  rows="5"
                  v-model="post.body">
          {{post.body}}
        </textarea>
      </div>

      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </section>
</template>

<script>
  import axios from 'axios'
  export default {
    data() {
      return {
        post: {}
      }
    },
    methods: {
      submit() {
        axios.post(`https://jsonplaceholder.typicode.com/posts`, this.post)
          .then((response) => {
            this.$router.push('/')
          })
          .catch((err) => console.log(err))
      }
    }
  }
</script>
