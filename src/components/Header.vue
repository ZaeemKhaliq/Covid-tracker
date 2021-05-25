<template>
  <div class="header-container">
    <div class="text-container">
      <h1 class="heading">COVID TRACKER</h1>
      <p>Country wise statistics about the coronavirus</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style lang="scss" scoped>
.header-container {
  min-height: calc(100vh - 65vh);
  background-color: rgb(250, 46, 46);
  display: flex;
  color: white;
  flex-direction: column;
  justify-content: center;
}
.text-container {
  width: 90%;
  margin: 0 auto;
}
.heading {
  margin: 0;
}
</style>
