<template>
  <div class="apps-container">
    <the-header />

    <main>
      <nuxt-child />
    </main>
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: "All the MiniApps",
    };
  },
};
</script>

<style scoped>
.apps-container {
  height: 100%;
  display: flex;
  flex-direction: column;
}

.apps-container > main {
  flex: 1;
  width: 100%;
}

main {
  max-width: 90vw;
  margin: 0 auto;
}
</style>
