<template>
  <Container animate="true" accessible-line-length="true">
    <h1 slot="headline" tabindex="-1">Blog</h1>
    <ul class="o-list-reset">
      <li v-for="post in posts" :key="post.sys.id" class="u-marginBottomLarge">
        <Post :post="post" :show-excerpt="true" :show-date="true" :level="2" :include-link="true" />
      </li>
    </ul>
    <PaginationActions :next-page="nextPage"></PaginationActions>
  </Container>
</template>

<script>
import Container from '~/components/Container.vue';
import Post from '~/components/Post.vue';
import PaginationActions from '~/components/PaginationActions.vue';
import { createPage } from '~/lib/basepage.js';

export default createPage({
  async fetch({ app }) {
    await app.contentful.getPosts();
  },
  computed: {
    nextPage() {
      return '/blog/page/2';
    },
    posts() {
      return this.$store.state.posts.list.slice(0, 5);
    }
  },
  head() {
    return {
      title: 'Blog | Stefan Judis Web Development',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: `Writings on web development including mainly JavaScript, web performance and accessibility.`
        }
      ]
    };
  },
  components: {
    Container,
    Post,
    PaginationActions
  }
});
</script>
