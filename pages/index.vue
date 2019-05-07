<template>
  <section class="container">

    <div class="row">
      <nuxt-link :to="{name: 'posts-new'}" class="btn btn-success float-right">
        + Adicionar
      </nuxt-link>
    </div>

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
        <tr v-for="post in posts">
          <td>{{post.id}}</td>
          <td>{{post.title}}</td>
          <td>{{post.body}}</td>
          <td>
            <nuxt-link
              :to="{name: 'posts-id', params: {id: post.id}}"
              :key="'view-post' + post.id">
              View
            </nuxt-link>

            <nuxt-link
              :to="{name: 'posts-edit-id', params: {id: post.id}}"
              :key="'edit-post'+ post.id">
              Edit
            </nuxt-link>

            <a href="#" @click="remove(post.id)">
              Delete
            </a>
          </td>
        </tr>
      </tbody>
    </table>
  </section>
</template>

<script>
  import _ from 'lodash'
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
    },
    methods: {
      remove(id) {
        axios.delete(`https://jsonplaceholder.typicode.com/posts/${id}`)
          .then(response => {
            if (response.status === 200) {
              this.posts = _.remove(this.posts, function(element) {
                return element.id !== id;
              })
            }
          });
      }
    }
  }
</script>

