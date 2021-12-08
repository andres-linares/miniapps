<template>
  <div>
    <ul>
      <li v-for="fact in facts" :key="fact._id">
        <p>{{ fact.text }}</p>
      </li>

      <li v-show="loading" class="loading">
        <p>Please wait while we interview some kitties...</p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'CatsFacts',
  data() {
    return {
      facts: [],
      loading: true,
      lastTimeout: null,
    }
  },
  created() {
    this.$store.commit('setTitle', this.$metaInfo.title);

    this.fetchFact();
  },
  beforeDestroy() {
    clearTimeout(this.lastTimeout);
  },
  methods: {
    async fetchFact() {
      const url = 'https://cat-fact.herokuapp.com/facts/random';

      try {
        const response = await fetch(url);
        const data = await response.json();

        const isUnique = !this.facts.find(x => x._id === data._id);

        if (isUnique) this.facts.push(data);
      } catch {}

      const lastfact = this.facts[this.facts.length - 1].text;

      this.lastTimeout = setTimeout(() => {
        this.fetchFact();
      }, lastfact.length * 60);
    }
  },
  head() {
    return {
      title: 'Cats Facts'
    }
  }
}
</script>

<style scoped>
ul {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(30ch, 1fr));
  column-gap: 1.25rem;
  row-gap: 1.75rem;
}

li {
  background: #99d98c2e;
  border: 1px solid #92ea7f7a;
  box-shadow: 1px 1px 3px #99d98c44;
  border-radius: 1.5rem 0 0.75rem 0;
  padding: 1rem 1.5rem;
}

li.loading {
  background: transparent;
}

p {
  line-height: 1.48;
  font-size: 1.1rem;
  font-style: italic;
  letter-spacing: 0.03em;
}
</style>
