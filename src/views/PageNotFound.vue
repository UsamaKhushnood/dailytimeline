<template>
  <div class="main-container text-center pageNotFound">
    <div class="w-100">
      <h1>OOPS! 404</h1>
      <h2>
        The page you're looking for <br />
        is not avaiable
      </h2>
    </div>
  </div>
</template>
<script>
export default {
  name: "PageNotFound",
};
</script>
<style lang="scss" scoped>
.pageNotFound {
  height: 400px;
  display: flex;
  justify-items: center;
  align-items: center;
  h1 {
    font-size: 50px;
  }
}
</style>
