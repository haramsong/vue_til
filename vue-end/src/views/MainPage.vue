<template>
  <div class="main list-container contents">
    <h1 class="page-header">Today I Learned</h1>
    <loading-spinner v-if="isLoading"></loading-spinner>
    <ul v-else>
      <PostListItem
        v-for="postItem in postItems"
        :key="postItem._id"
        :postItem="postItem"
      ></PostListItem>
    </ul>
  </div>
</template>

<script>
import { fetchPosts } from '@/api/index';
import LoadingSpinner from '@/components/common/LoadingSpinner.vue';
import PostListItem from '@/components/posts/PostListItem.vue';

export default {
  components: {
    PostListItem,
    LoadingSpinner,
  },
  data() {
    return {
      postItems: [],
      isLoading: false,
    };
  },
  methods: {
    async fetchData() {
      this.isLoading = true;
      const { data } = await fetchPosts();
      this.isLoading = false;
      this.postItems = data.posts;
    },
  },
  created() {
    this.fetchData();
  },
};
</script>

<style></style>
