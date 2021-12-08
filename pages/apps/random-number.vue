<template>
  <div>
    <form @submit.prevent="onSubmit">
      <div class="control">
        <label for="minNumber">Min number</label>
        <input
          type="number"
          id="minNumber"
          v-model.number="minNumber"
          :max="maxNumber - 1"
          required
        />
      </div>

      <div class="control">
        <label for="maxNumber">Max number</label>
        <input
          type="number"
          id="maxNumber"
          v-model.number="maxNumber"
          :min="minNumber + 1"
          required
        />
      </div>

      <button type="submit" :disabled="generating">Generate</button>
    </form>

    <output class="output">{{ randomNumber || randomNumberFinal }}</output>
  </div>
</template>

<script>
export default {
  name: "RandomNumber",
  data() {
    return {
      minNumber: 1,
      maxNumber: 9,
      randomNumber: null,
      randomNumberFinal: null,
      generating: false,
      generateInterval: null
    };
  },
  created() {
    this.$store.commit("setTitle", this.$metaInfo.title);
  },
  methods: {
    getRandom() {
      const randomZeroToOne = Math.random();
      const delta = this.maxNumber - this.minNumber;
      const randomSpace = randomZeroToOne * delta;

      return Math.round(randomSpace + this.minNumber);
    },
    onSubmit() {
      this.generating = true;
      this.randomNumberFinal = this.getRandom();
      this.animateGuess();
    },
    animateGuess() {
      let tries = 0;
      const maxTries = 27;

      this.generateInterval = setInterval(() => {
        if (tries >= maxTries) {
          clearInterval(this.generateInterval);
          this.randomNumber = null;
          this.generating = false;
        }

        this.randomNumber = this.getRandom();
        tries++;
      }, 33);
    }
  },
  head() {
    return {
      title: "Random Number",
    };
  },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  align-items: center;
  row-gap: 2vh;
  max-width: 20rem;
  margin: 0 auto;
}

form button {
  margin-left: auto;
  margin-top: 1.5vh;
  background: var(--color-primary);
  border: none;
  padding: 0.25em 1em;
  font-weight: 600;
  letter-spacing: 0.025em;
  border-radius: 0.15em;
}

.control {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.control label {
  font-weight: 600;
  margin-bottom: 0.25rem;
}

.output {
  font-size: clamp(3rem, 5vw, 6rem);
  display: block;
  text-align: center;
  margin-top: 5vh;
  border-radius: 50%;
}
</style>
