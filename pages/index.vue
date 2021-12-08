<template>
  <div>
    <ul>
      <li>
        <article>
          <h6>Chronometer</h6>

          <p>A simple chronometer with a play and stop button</p>
        </article>
      </li>
    </ul>
  </div>
</template>

<script>
export default {}
</script>

<style scoped>
ul {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr));
}

article h6 {
  font-size: 1.25rem;
  font-weight: 700;
}
</style>
