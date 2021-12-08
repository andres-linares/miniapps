<template>
  <div class="chronometer">
    <output class="output">{{ ellapsedTime }}</output>

    <div class="actions">
      <button @click="start" class="start-button" :disabled="currentTime">
        <i class="material-icons">play_arrow</i>
      </button>
      <button @click="stop" class="stop-button" :disabled="!currentTime">
        <i class="material-icons">stop</i>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Chronometer",
  data() {
    return {
      startTime: null,
      interval: null,
      currentTime: null,
    };
  },
  computed: {
    ellapsedTime() {
      if (!this.currentTime) {
        return "0:00:00.00";
      }

      const ellapsedTimeInMs = this.currentTime - this.startTime;
      const ellapsedTime = ellapsedTimeInMs / 1000;

      let hundreths = Math.floor((ellapsedTimeInMs / 10) % 100);
      let seconds = Math.floor(ellapsedTime % 60);
      let minutes = Math.floor((ellapsedTime / 60) % 60);
      let hours = Math.floor(ellapsedTime / 60 / 60);

      hundreths = hundreths.toString().padStart(2, "0");
      seconds = seconds.toString().padStart(2, "0");
      minutes = minutes.toString().padStart(2, "0");

      return `${hours}:${minutes}:${seconds}.${hundreths}`;
    },
  },
  created() {
    this.$store.commit('setTitle', this.$metaInfo.title);
  },
  beforeDestroy() {
    if (this.interval) clearInterval(this.interval);
  },
  methods: {
    start() {
      this.startTime = performance.now();

      this.interval = setInterval(() => {
        this.currentTime = performance.now();
      }, 10);
    },
    stop() {
      clearInterval(this.interval);

      this.startTime = null;
      this.currentTime = null;
    },
  },
  head() {
    return {
      title: "Chronometer",
    };
  },
};
</script>

<style scoped>
.chronometer {
  display: grid;
  place-items: center;
}

.output {
  font-family: "Roboto Mono", monospace;
  font-size: clamp(1.5rem, 4vw, 3.5rem);
}

button {
  cursor: pointer;
  height: 2.75rem;
  width: 2.75rem;
  border-radius: 50%;
  display: grid;
  place-items: center;
  border: 1px solid #dadada;
  transition: transform 250ms ease-out;
}

button:disabled {
  opacity: 0.45;
  cursor: default;
}

button:disabled:hover,
button:disabled:focus {
  transform: scale(0.95);
}

button:hover,
button:focus {
  transform: scale(1.2);
}

button:focus {
  outline-offset: 0.25rem;
}

.start-button {
  background: #0e990f;
  color: #fff;
}

.stop-button {
  background: #B8030E;
  color: #fff;
}

.actions {
  margin-top: 2.5vh;
  display: flex;
  align-items: center;
  column-gap: 5vw;
}
</style>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto+Mono:wght@400&display=swap");
@import url("https://fonts.googleapis.com/icon?family=Material+Icons");
</style>
