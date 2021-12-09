<template>
  <ul>
    <li v-for="index in 50" :key="index">
      <img
        :src="`https://picsum.photos/300?random=${index}`"
        alt=""
        :style="{
          '--animation-time': getRandomTime(),
          '--max-rotation': getMaxRotation(),
          '--timing-function': getTimingFunction(),
          '--min-scale': getMinScale(),
          '--max-scale': getMaxScale(),
        }"
      />
    </li>
  </ul>
</template>

<script>
export default {
  name: "RotatoryImages",
  created() {
    this.$store.commit("setTitle", this.$metaInfo.title);
  },
  methods: {
    getRandomTime() {
      return Math.round(Math.random() * 3000 + 3500) + "ms";
    },
    getMaxRotation() {
      const maxAngle = Math.round(Math.random() * 1000 + 360);

      return Math.random() < 0.5 ? `${maxAngle}deg` : `-${maxAngle}deg`;
    },
    getTimingFunction() {
      const x1 = Math.random();
      const y1 = Math.random();
      const x2 = Math.random();
      const y2 = Math.random();

      return `cubic-bezier(${x1}, ${y1}, ${x2}, ${y2})`;
    },
    getMinScale() {
      return Math.random() * 0.5;
    },
    getMaxScale() {
      return Math.random() + 0.75;
    },
  },
  head() {
    return {
      title: "Rotatory Images",
    };
  },
};
</script>

<style scoped>
ul {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(10rem, 1fr));
  grid-auto-rows: 10rem;
  overflow: hidden;
  box-shadow: 0 0 1px 2px #000;
}

li {
  overflow: hidden;
  background: #000000c5;
  border: 1px solid #000;
}

img {
  animation: rotate var(--animation-time, 1500ms) var(--timing-function, linear)
    infinite alternate;
  border-radius: 50%;
  border: none;
}

@keyframes rotate {
  from {
    transform: rotate(0) scale(var(--min-scale, 0.1));
  }

  to {
    transform: rotate(var(--max-rotation, 360deg)) scale(var(--max-scale, 2));
  }
}
</style>
