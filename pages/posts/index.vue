<template>
  <div class="posts-page">
    <section class="post-list">
      <PostList :posts="loadedPosts" />
    </section>
  </div>
</template>

<script>
import PostList from "@/components/Posts/PostList";
export default {
  components: {
    PostList,
  },
  computed: {
    loadedPosts() {
      return this.$store.getters.loadedPosts;
    },
  },
};
</script>

<style scoped>
.posts-page {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>