<template>
  <div class="c-loadTime">
    <Icon name="Stopwatch"></Icon>
    <div class="c-loadTime__text">
      <div class="c-loadTime__number"></div>
      <div class="c-loadTime__title">Load time</div>
    </div>
    <script>
      // shamelessly stolen from Tim Kadlec
      // TODO give credits
      window.onload = function () {
        setTimeout(function () {
          window.performance = window.performance || window.mozPerformance || window.msPerformance || window.webkitPerformance || {}
          var t = performance.timing || {}

          if (!t) {
            return
          }
          var start = t.navigationStart
          var end = t.loadEventEnd
          var loadTime = (end - start) / 1000
          var numberContainer = document.querySelector('.c-loadTime__number')
          numberContainer.innerHTML += loadTime + 's'
          document.querySelector('.c-loadTime').classList.add('is-loaded')
        }, 0)
      }
    </script>
  </div>
</template>

<script>
export default {
  components: {
    Icon: () => import('~/components/Icon.vue')
  }
};
</script>


<style>
.c-loadTime {
  display: none;
  align-items: center;
  justify-content: center;
  padding: 2em;

  @media (min-width: 47em) {
    position: absolute;
    bottom: 0;
    right: 2em;
    bottom: 1.5em;
    width: 8em;
    padding: 0.5em 1em 0.5em 0.75em;
    box-shadow: var(--shadow-floating-thing);
    justify-content: space-between;
  }

  &.is-loaded {
    display: flex;
  }

  .icon-Stopwatch svg {
    display: block;
    width: 2em;
    height: 2em;
    margin-right: 0.5em;
  }

  &__number {
    font-size: 1.25em;
    font-size: bolder;
    line-height: 1;
    color: var(--c-text-contrast);
  }

  &__title {
    font-size: 0.75em;
    line-height: 1.25;
    color: var(--c-highlight);
  }
}
</style>
