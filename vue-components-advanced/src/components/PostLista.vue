<template>
  <div>

    <h2>Lista de posts</h2>

    <PostListaItem
    v-for="post in posts"
    :key="post.id"
    :post="post"
    >
      <slot :meuPost="post"></slot>
    </PostListaItem>

  </div>
</template>

<script>
import PostListaItem from './PostListaItem.vue'
  export default {
    components: {
      PostListaItem
    },
    props: {
      posts: {
        type: Array,
        required: true
      }
    }
  }
</script>