<template>
  <div>
    <the-header />

    <ul>
      <li v-for="app in apps" :key="app.url">
        <nuxt-link :to="app.url">
          <article>
            <img :src="app.preview" alt="preview">

            <main>
              <h6>{{ app.title }}</h6>

              <p>{{ app.description }}</p>
            </main>
          </article>
        </nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script>
import apps from '@/assets/json/apps.json';

export default {
  name: "Index",
  data() {
    return {
      apps: apps,
    };
  },
  created() {
    this.$store.commit('setTitle', 'The Collection');
  },
  head() {
    return {
      title: 'MiniApps! - Collection'
    }
  }
};
</script>

<style scoped>
ul {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(16rem, 1fr));
  column-gap: clamp(1rem, 2vw, 1.75rem);
  row-gap: 1.5rem;
  margin: 0 3vw 6vh 3vw;
}

a {
  display: block;
  height: 100%;
  text-decoration: none;
  color: inherit;
}

article {
  overflow: hidden;
  border-radius: 0.75rem;
  box-shadow: 2px 2px 5px #0000000e, 0 0 0 1px #99d98c54;
  height: 100%;
  display: flex;
  flex-direction: column;
}

article main {
  padding: 1rem 0.75rem 1.25rem;
  background: #f8f8f8;
  flex: 1;
}

article img {
  height: 13rem;
  width: 100%;
  object-fit: contain;
}

article h6 {
  font-size: 1.25rem;
  font-weight: 700;
  margin-bottom: 0.35em;
  letter-spacing: 0.01em;
}
</style>
