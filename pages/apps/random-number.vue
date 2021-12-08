<template>
  <div>
    <h1>Random Number</h1>

    <form @submit.prevent="onSubmit">
      <label for="minNumber">Min number</label>
      <input
        type="number"
        id="minNumber"
        v-model.number="minNumber"
        :max="maxNumber - 1"
        required
      />

      <label for="maxNumber">Max number</label>
      <input
        type="number"
        id="maxNumber"
        v-model.number="maxNumber"
        :min="minNumber + 1"
        required
      />

      <button type="submit">Generate</button>
    </form>

    <output>{{ randomNumber }}</output>
  </div>
</template>

<script>
export default {
  name: "RandomNumber",
  data() {
    return {
      minNumber: 1,
      maxNumber: 9,
      randomNumber: null
    };
  },
  methods: {
    onSubmit() {
      const randomZeroToOne = Math.random();

      const delta = this.maxNumber - this.minNumber;
      const randomSpace = randomZeroToOne * delta;

      this.randomNumber = Math.round(randomSpace + this.minNumber);
    },
  },
  head() {
    return {
      title: 'Random Number'
    }
  }
};
</script>

<style></style>
