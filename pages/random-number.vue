<template>
  <div>
    <h1>Random Number</h1>

    <form @submit.prevent="">
      <label for="minNumber">Min number</label>
      <input type="number" name="" id="minNumber">

      <label for="maxNumber">Max number</label>
      <input type="number" name="" id="maxNumber">
    </form>
  </div>
</template>

<script>
export default {
  name: 'RandomNumber'
}
</script>

<style>

</style>
