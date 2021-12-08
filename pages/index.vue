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

<style>
@import url("https://fonts.googleapis.com/css2?family=Nunito:wght@400;700&family=Roboto+Mono&display=swap");

* {
  margin: 0;
  padding: 0;
}

ul,
ol {
  list-style: none;
}

html,
body {
  height: 100%;
  font-family: 'Nunito', sans-serif;
}
</style>
