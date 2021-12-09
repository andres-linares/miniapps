<template>
  <div class="container">
    <div class="clock">
      <span class="center"></span>

      <span class="hour" :style="{ '--rotation': hourRotation }"></span>
      <span class="minute" :style="{ '--rotation': minuteRotation }"></span>
      <span class="second" :style="{ '--rotation': secondRotation }"></span>
    </div>
    <div style="text-align: center; align-self: start;">
      {{ new Date().toTimeString() }}
    </div>
  </div>
</template>

<script>
export default {
  name: "Clock",
  data() {
    return {
      currentHour: 0,
      currentMinute: 0,
      currentSecond: 0,
      currentMilliseconds: 0,
      interval: null,
    };
  },
  computed: {
    hourRotation() {
      const minutePercentage = this.currentMinute / 60;

      const deltaAngle = 360 / 12;
      const finalAngle = deltaAngle * (this.currentHour + minutePercentage);

      return finalAngle + "deg";
    },
    minuteRotation() {
      const secondPercentage = this.currentSecond / 60;

      const deltaAngle = 360 / 60;
      const finalAngle = deltaAngle * (this.currentMinute + secondPercentage);

      return finalAngle + "deg";
    },
    secondRotation() {
      const millisecondsPercentage = this.currentMilliseconds / 1000;

      const deltaAngle = 360 / 60;
      const finalAngle = deltaAngle * (this.currentSecond + millisecondsPercentage);

      return finalAngle + "deg";
    },
  },
  created() {
    this.$store.commit('setTitle', this.$metaInfo.title);
    this.getTime();

    this.interval = setInterval(this.getTime, 10);
  },
  beforeDestroy() {
    clearInterval(this.interval);
  },
  methods: {
    getTime() {
      const date = new Date();

      this.currentHour = date.getHours() % 12;
      this.currentMinute = date.getMinutes();
      this.currentSecond = date.getSeconds();
      this.currentMilliseconds = date.getMilliseconds();
    }
  },
  head() {
    return {
      title: "Clock",
    };
  },
};
</script>

<style scoped>
.container {
  height: 100%;
  display: grid;
  place-items: center;
}

.clock {
  width: 45vmin;
  height: 45vmin;
  border-radius: 50%;
  background: #f8f8f2;
  position: relative;
  box-sizing: border-box;
  border: 0.75vmin solid #000;
}

@media screen and (orientation: portrait) {
  .clock {
    width: 60vmin;
    height: 60vmin;
  }
}

.clock .center {
  position: absolute;
  width: 0.8vmin;
  height: 0.8vmin;
  background: #dbd81d;
  border-radius: 50%;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 10;
}

.clock .hour {
  position: absolute;
  width: 0.75vmin;
  height: 27%;
  background: #000;
  top: 23%;
  left: 50%;
  transform: translateX(-50%) rotate(var(--rotation, 0));
  transform-origin: bottom;
}

.clock .minute {
  position: absolute;
  width: 0.75vmin;
  height: 40%;
  background: #000;
  top: 10%;
  left: 50%;
  transform: translateX(-50%) rotate(var(--rotation, 0));
  transform-origin: bottom;
}

.clock .second {
  position: absolute;
  width: 0.25vmin;
  height: 43%;
  background: #000;
  top: 7%;
  left: 50%;
  transform: translateX(-50%) rotate(var(--rotation, 0));
  transform-origin: bottom;
}
</style>
