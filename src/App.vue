<template>
  <Header />
  <router-view />

  <Footer />
</template>

<script>
import Header from "./components/Header";
import Footer from "./components/Footer";

export default {
  name: "App",
  components: {
    Header,
    Footer,
  },
};
</script>

<style lang="scss">
#app {
  font-family: "Roboto", sans-serif;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  min-height: 100vh;
  min-width: 100vh;
}

body {
  margin: 0;
}
</style>
