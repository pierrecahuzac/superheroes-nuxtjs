<template>
  <div class="header">
    <h1>Super heroes characters list</h1>
  </div>
</template>

<script>
export default {
  name: "header",
};
</script>

<style>
.header {
  height: 200px;
  position: relative;
  @media (min-width: 750px) {
    height: 500px;
  }
}
</style>