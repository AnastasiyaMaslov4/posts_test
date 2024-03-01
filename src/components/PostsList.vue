<template>
  <div class="posts_list">
    <div v-if="appLoading"><p>Загрузка постов...</p></div>
    <Post v-else v-for="post in this.posts" :key="post.id" :postId="post.id" :title="post.title" :text="post.body" :users="this.users" :author="getAuthorName(post.userId)" :authorId="post.userId" v-on:favourited="addToFavourite(post.id)" @delete="deletePost(post.id)" @checkPost="checkPost(post.id)" :favourite="getFavourite(post)" :checkedPosts="this.updateCheckedPosts" @editedPost="editPost"/>
  </div>
</template>

<script>
import Post from './Post.vue'

export default {
  name: 'PostsList',
  components: {
        Post
      },
  props: {
    perPage: String,
    postTitleFilter: String,
    posts: Array,
    users: Array,
    appLoading: Boolean,
    favouritePosts: Array,
    clearCheckedPosts: false
  },
  emits: ['addToFavourite', 'deletePost', 'updateCheckedPosts', 'editedPost'],
  data() {
    return {
      chekedPosts: []
    }
  },
  methods: {
    getAuthorName(id) {
      let author = this.users.find(user => user.id === id);
      return author.name;
    },
    getFavourite(post) {
      if(this.favouritePosts.includes(post)) return true;
      else return false;
    },
    addToFavourite(postId) {
      this.$emit('addToFavourite', postId)
    },
    deletePost(postId) {
      this.$emit('deletePost', postId)
    },
    checkPost(postId) {
      if(this.clearCheckedPosts) this.chekedPosts = [];
      if(!this.chekedPosts.includes(postId)) this.chekedPosts.push(postId);
      else this.chekedPosts.splice(this.chekedPosts.indexOf(postId),1);
      this.$emit('updateCheckedPosts', this.chekedPosts);
    },
    editPost(post) {
      this.$emit('editedPost', post);
    }
  },
  computed: {
    updateCheckedPosts() {
      if(this.clearCheckedPosts) return [];
      else return this.chekedPosts;
    }
  }
}
</script>

<style scoped lang="scss">
.posts_list {
  width: 80%;
  display: flex;
  flex-direction: column;
  gap: 20px;
  margin: 0 auto;
}
</style>
