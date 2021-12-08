<template>
  <div ref="canvas">
  </div>
</template>

<script>
export default {
  name: 'PixelsFiller',
  data() {
    return {
      interval: null,
      userWantsToScroll: false
    }
  },
  created() {
    this.$store.commit('setTitle', this.$metaInfo.title);
  },
  mounted() {
    let lastScroll = 0;

    document.addEventListener('scroll', () => {
      const currentScroll = window.scrollY;

      if (lastScroll > currentScroll) {
        this.userWantsToScroll = true;
      } else {
        this.userWantsToScroll = false;
      }

      lastScroll = currentScroll;
    });

    this.interval = setInterval(() => {
      const spans = [];

      const totalSpans = this.$refs.canvas.childElementCount;
      const chunk = totalSpans < 1000 ? 20 : totalSpans < 5000 ? 10 : totalSpans < 10000 ? 5 : 3;

      for (let i = 0; i < chunk; i++) {
        const span = document.createElement('span');

        const h = 110;
        const s = Math.round(Math.random() * 70 + 30);
        const l = Math.round(Math.random() * 75 + 20);

        span.style.background = `hsl(${h}, ${s}%, ${l}%)`;

        spans.push(span);
      }

      this.$refs.canvas.append(...spans);
      if (!this.userWantsToScroll) window.scrollTo({ top: 999999 });
    }, 10);
  },
  beforeDestroy() {
    clearInterval(this.interval);
  },
  head() {
    return {
      title: 'Pixels Filler'
    }
  }
}
</script>

<style scoped>
div {
  width: 100%;
  height: 100%;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(1vmax, 1fr));
  grid-auto-rows: 1vmax;
  margin-bottom: 10vh;
}
</style>
