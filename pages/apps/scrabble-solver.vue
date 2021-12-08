<template>
  <div>
    <form @submit.prevent="onSubmit">
      <div class="control">
        <label for="lettersInput">Type your letters</label>
        <input
          type="text"
          v-model="letters"
          id="lettersInput"
          :disabled="loading"
        />
      </div>

      <button type="submit" class="button-primary" :disabled="loading">
        Find!
      </button>
    </form>

    <h3 v-if="words && words.length > 0">Results</h3>
    <ul>
      <li v-for="wordGroup in words" :key="wordGroup.length">
        <fieldset>
          <legend>{{ wordGroup.length }} letters</legend>

          <ul class="words-list">
            <li v-for="word in wordGroup.word_list" :key="word.word">
              {{ word.word }}
            </li>
          </ul>
        </fieldset>
      </li>
    </ul>

    <div></div>
  </div>
</template>

<script>
export default {
  name: "ScrabbleSolver",
  data() {
    return {
      letters: "",
      words: null,
      loading: false,
    };
  },
  created() {
    this.$store.commit("setTitle", this.$metaInfo.title);
  },
  methods: {
    async onSubmit() {
      if (this.loading) return;

      const url = `https://fly.wordfinderapi.com/api/search?dictionary=wwf2&word_sorting=points&group_by_length=true&letters=${this.letters}&page_size=50`;
      this.loading = true;

      try {
        const response = await fetch(url);
        const data = await response.json();

        this.words = data.word_pages;
      } catch (e) {
        this.words = [];
      }
      this.loading = false;
    },
  },
  head() {
    return {
      title: "Scrabble Solver",
    };
  },
};
</script>

<style scoped>
form {
  margin-left: auto;
  max-width: 14rem;
  display: flex;
  flex-direction: column;
  margin-bottom: 5vh;
}

.control {
  display: flex;
  flex-direction: column;
}

.control label {
  font-weight: 600;
  margin-bottom: 0.1em;
}

button {
  margin-top: 1rem;
  margin-left: auto;
}

h3 {
  text-align: center;
  margin-bottom: 0.5em;
}

fieldset {
  padding: 0.5rem 2rem 1rem 0.5rem;
  margin-bottom: 1.5vh;
}

legend {
  font-weight: 700;
  font-size: 1.2rem;
  letter-spacing: -0.012em;
}

.words-list {
  display: flex;
  flex-wrap: wrap;
  column-gap: 0.4rem;
  row-gap: 0.5rem;
  font-size: 1.125rem;
  text-transform: uppercase;
  letter-spacing: 0.035em;
}

.words-list li {
  background: var(--color-primary);
  border-radius: 100px;
  padding: 0.25em 0.9em;
}
</style>
