<template>
  <div class="footer">
    <p class="copyright">Copyright &copy; Covid Tracker</p>
    <p class="author">
      Created by
      <a
        href="https://github.com/ZaeemKhaliq"
        target="_blank"
        rel="noopener noreferrer"
        >Zaeem Khaliq</a
      >
    </p>
  </div>
</template>

<script>
export default {
  name: "Footer",
};
</script>

<style lang="scss" scoped>
.footer {
  min-height: calc(100vh - 85vh);
  background-color: black;
  color: white;
  display: flex;
  flex-direction: column;
}

.copyright {
  text-align: center;
}

.author {
  text-align: center;

  & > a {
    text-decoration: none;
    color: rgb(76, 107, 248);
  }
}
</style>
