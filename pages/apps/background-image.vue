<template>
  <div class="app-container" ref="container">
    <button @click="setImage">
      Get my Image!
    </button>
  </div>
</template>

<script>
export default {
  created() {
    this.$store.commit('setTitle', this.$metaInfo.title);
  },
  methods: {
    setImage() {
      const container = this.$refs.container;
      const density = window.devicePixelRatio;
      const width = Math.round(container.clientWidth * density);
      const height = Math.round(container.clientHeight * density);

      const url = `https://picsum.photos/${width}/${height}?random=${Math.random()}`;

      container.style.backgroundImage = `url(${url})`;
    }
  },
  head() {
    return {
      title: 'Random Image'
    }
  }
}
</script>

<style scoped>
.app-container {
  height: 100%;
  display: grid;
  place-items: center;
  background-size: cover;
}

button {
  background: #000;
  border: 2px solid #fff;
  border-radius: 0.15em;
  color: #fff;
  padding: 0.25em 1em;
}
</style>
