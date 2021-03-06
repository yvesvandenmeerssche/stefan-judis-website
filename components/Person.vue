<template>
  <div class="c-person u-marginTopLarge">
    <div class="c-person__image">
      <div>
        <lazy-image class="c-person__image" :asset="person.fields.profilePhoto" :ratio="1" :load="true"></lazy-image>
        <ul class="c-person__social">
          <li>
            <a href="https://twitter.com/stefanjudis" rel="me" aria-label="Follow me on Twitter">
              <Icon name="Twitter"></Icon>
            </a>
          </li>
          <li>
            <a href="https://github.com/stefanjudis" rel="me" aria-label="Follow me on GitHub">
              <Icon name="GitHub"></Icon>
            </a>
          </li>
          <li>
            <a href="https://www.instagram.com/stefans_little_planet/" rel="me" aria-label="Follow me on Instagram">
              <Icon name="Instagram"></Icon>
            </a>
          </li>
        </ul>
      </div>
    </div>
    <div class="c-person__details">
      <div v-html="bio"></div>
      <p>I also <nuxt-link to="/staying-up-to-date/">read a lot of newsletters and listen to a few podcasts</nuxt-link>, document <nuxt-link to="/today-I-learned/">my web dev learnings constantly</nuxt-link> and write <nuxt-link to="/newsletter/">a monthly newsletter</nuxt-link>.</p>
    </div>
  </div>
</template>

<script>
import marked from '~/plugins/marked.js';
import LazyImage from '~/components/LazyImage.vue';

export default {
  computed: {
    bio: function() {
      return marked(this.person.fields.biography);
    }
  },
  components: {
    Icon: () => import('~/components/Icon.vue'),
    LazyImage
  },
  props: ['person']
};
</script>

<style>
.c-person {
  display: flex;
  flex-direction: column;
  align-items: center;

  box-shadow: var(--shadow-person);
}

@media (min-width: 45.5em) {
  .c-person {
    flex-direction: row;
  }
}

.c-person__details {
  padding: 1em;

  @media (min-width: 56em) {
    font-size: 1.125em;
  }
}

.c-person__details p {
  margin-top: 0;
}

.c-person__image {
  width: 100%;
  overflow: hidden;
  position: relative;

  border-radius: 0.125em 0.25em 0 0;
  overflow: hidden;

  @media (min-width: 45.5em) {
    margin: 0 1em 0 0;
    flex: 0 0 50%;
    flex-direction: row;
    border-radius: 0;
  }

  @media (min-width: 56em) {
    flex: 0 0 33.333%;
  }
}

.c-person__social {
  position: absolute;
  bottom: 1em;
  left: 0;
  z-index: 0;
  color: #fff;
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: row;

  background: #fff;
}

.c-person__social li {
  &:nth-child(1) {
    a:hover {
      background: var(--blue-dark);
    }
  }

  &:nth-child(2) {
    a:hover {
      background: var(--green-dark);
    }
  }

  &:nth-child(3) {
    a:hover {
      background: var(--red-dark);
    }
  }
}

.c-person__social li a {
  display: block;
  padding: 0.5em;

  &:hover {
    background: var(--c-highlight);

    svg {
      fill: #fff;
    }
  }
}

.c-person__social svg {
  display: block;
  width: 1.5em;
  height: 1.5em;

  left: 0;
  top: -0.125em;

  fill: var(--dark-grey);
}
</style>
