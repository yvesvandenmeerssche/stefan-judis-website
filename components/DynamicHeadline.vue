<script>
export default {
  props: ['level', 'url'],
  render: function(h) {
    return h(
      'h' + this.level,
      {
        class: `o-headline-${this.level}`,
        attrs: {
          ...(this.level === 1 && { tabindex: '-1' })
        }
      },
      [
        this.url
          ? this.url.startsWith('http://')
            ? h( 'a', { attrs: { href: this.url } }, this.$slots.default)
            : h('nuxt-link', { props: { to: this.url } }, this.$slots.default)
          : this.$slots.default
      ]
    );
  }
};
</script>
