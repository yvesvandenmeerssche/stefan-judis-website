<template>
  <div class="c-markdown" v-if="renderedHtml" v-html="renderedHtml"></div>
</template>

<script>
import marked from '~/plugins/marked.js';

export default {
  props: ['markdown'],
  computed: {
    renderedHtml() {
      return marked(this.markdown);
    }
  }
};
</script>

<style>
.c-markdown {
  blockquote {
    position: relative;
    margin: 0;
    padding: 0.5em 0.5em 0.5em 2em;
    font-style: italic;

    p {
      &::before {
        position: absolute;

        left: 0;
        top: 0;

        font-family: 'Georgia', serif;
        font-size: 3em;
        font-weight: normal;
        content: '“';
      }
    }
  }

  code {
    font-size: 1.125em;
    font-family: monospace;
    font-weight: 400;
    line-height: 1.5;
    padding: 0.125em;
    color: var(--c-highlight);
    border-radius: 0.25em;
  }

  img {
    display: block;
    margin: 0 auto;
  }

  hr {
    border-color: var(--c-highlight);
  }
}
</style>
