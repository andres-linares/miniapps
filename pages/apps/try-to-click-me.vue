<template>
  <div :class="{ clicked }">
    <button
      ref="button"
      class="button-primary"
      @mouseenter="moveButton"
      @click="clicked = true"
      tabindex="-1"
    >
      <i class="material-icons">touch_app</i>
    </button>
  </div>
</template>

<script>
export default {
  name: "TryToClickMe",
  data() {
    return {
      clicked: false,
    };
  },
  created() {
    this.$store.commit("setTitle", this.$metaInfo.title);
  },
  methods: {
    moveButton() {
      const top = Math.random() * 90 + 5;
      const left = Math.random() * 90 + 5;

      const button = this.$refs.button;
      button.style.top = `${top}%`;
      button.style.left = `${left}%`;
    },
  },
  head() {
    return {
      title: "Try To Click Me!",
    };
  },
};
</script>

<style scoped>
div {
  height: 100%;
  outline: 1px solid var(--color-primary);
  position: relative;
}

div.clicked {
  background: #000000cc;
}

div.clicked::before {
  position: absolute;
  content: "You won";
  font-size: 2rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: #fff;
}

button {
  position: absolute;
  width: 44px;
  height: 44px;
  border-radius: 50%;
  top: 50%;
  left: 50%;
  padding: 0;
  display: grid;
  place-items: center;
  transition: 250ms ease-in-out;
  box-shadow: 3px 3px 7px 1px #00000014;
}

button:hover {
  transform: scale(0.75);
}
</style>

<style>
@import url("https://fonts.googleapis.com/icon?family=Material+Icons");
</style>
