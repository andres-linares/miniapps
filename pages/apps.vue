<template>
  <div>
    <header>
      <nuxt-link class="logo" to="/">
        MiniApps!
      </nuxt-link>

      <h1 class="current-page">{{ title }}</h1>
    </header>

    <main>
      <nuxt-child />
    </main>
  </div>
</template>

<script>
import { mapState } from 'vuex';

export default {
  head() {
    return {
      title: 'All the MiniApps'
    }
  },
  computed: {
    ...mapState(['title'])
  }
}
</script>

<style scoped>
header {
  min-height: 4rem;
  background: var(--color-primary);
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 2vw;
  box-shadow: 2px 2px 6px #99d98c45;
  margin-bottom: 2vh;
}

header .logo {
  letter-spacing: 0.06em;
  font-weight: 700;
  color: inherit;
  text-decoration: none;
}

header .current-page {
  font-size: var(--font-size-l);
  letter-spacing: 0.02em;
  font-weight: 400;
}

main {
  max-width: 90vw;
  margin: 0 auto;
}
</style>
