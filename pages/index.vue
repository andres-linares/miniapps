<template>
  <div>
    <ul>
      <li v-for="app in apps" :key="app.url">
        <nuxt-link :to="app.url">
          <article>
            <img alt="preview">

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
export default {
  name: "Index",
  data() {
    return {
      apps: [
        {
          title: "Chronometer",
          description: "A simple chronometer with a play and stop button",
          url: "/apps/chronometer",
        },
        {
          title: "Random number",
          description:
            "A random number generator with a bottom and upper limit",
          url: "/apps/random-number",
        },
        {
          title: "Random Image",
          description: "A random image generator for your background",
          url: "/apps/random-image",
        },
      ],
    };
  },
};
</script>

<style scoped>
ul {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(16rem, 1fr));
  column-gap: 1rem;
  row-gap: 1.5rem;
}

article {
  background: #eaeaea;
}

article main {
  padding: 0.25rem 0.5rem;
}

article h6 {
  font-size: 1.25rem;
  font-weight: 700;
}
</style>
