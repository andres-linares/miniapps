<template>
  <div class="grid-center">
    <div class="meme-container">
      <button @click="previous" class="previous">
        <i class="material-icons">navigate_before</i>
      </button>
      <img :src="currentMeme" alt="">
      <button @click="next" class="next">
        <i class="material-icons">navigate_next</i>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MemeTemplates',
  data() {
    return {
      memes: [],
      index: 0
    }
  },
  computed: {
    currentMeme() {
      return this.memes[this.index]?.url;
    }
  },
  created() {
    this.$store.commit('setTitle', this.$metaInfo.title);

    this.fetchMemes();
  },
  methods: {
    async fetchMemes() {
      const url = 'https://api.imgflip.com/get_memes';

      try {
        const response = await fetch(url);
        const data = await response.json();

        this.memes = data.data.memes;
      } catch {}
    },
    previous() {
      this.index = this.index - 1 < 0 ? this.memes.length - 1 : this.index - 1;
    },
    next() {
      this.index = this.index + 1 > this.memes.length - 1 ? 0 : this.index + 1;
    }
  },
  head() {
    return {
      title: 'Meme Templates'
    }
  }
}
</script>

<style scoped>
.meme-container {
  position: relative;
  width: 80vw;
}

button {
  position: absolute;
  width: 44px;
  height: 44px;
  border: 2px solid #000;
  background: #fff;
  border-radius: 50%;
  display: grid;
  place-items: center;
  opacity: 0.5;
  transition: opacity 250ms ease-out;
}

button:hover,
button:focus {
  opacity: 0.9;
}

.previous,
.next {
  top: 50%;
  transform: translateY(-50%);
}

.previous {
  left: 1rem;
}

.next {
  right: 1rem;
}

img {
  height: 85vh;
  object-fit: contain;
  margin: 0 auto;
}
</style>

<style>
@import url("https://fonts.googleapis.com/icon?family=Material+Icons");
</style>
