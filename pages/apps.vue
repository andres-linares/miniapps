<template>
  <div>
    <header>
      <div class="logo">
        MiniApps!
      </div>
    </header>

    <main>
      <nuxt-child />
    </main>
  </div>
</template>

<script>
export default {

}
</script>

<style scoped>
header {
  min-height: 4rem;
  background: #99d98c;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 2vw;
  box-shadow: 2px 2px 6px #99d98c45;
  margin-bottom: 2vh;
}

header .logo {
  letter-spacing: 0.06em;
  font-weight: 700;
}

main {
  max-width: 90vw;
  margin: 0 auto;
}
</style>
