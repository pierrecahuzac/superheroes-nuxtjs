<template>
  <div class="loading-container">
    <img class="img" src="~/assets/Loading_icon_with_fade.png" alt="" />
  </div>
</template>

<script>
export default {
  name: "Loading",
};
</script>

<style scoped>
.loading-container {
  display: flex;
  justify-content: center;
  z-index: 2;
  align-items: center;
  width: 100%;
  min-height: 100vh;
  background-color: white;
}
/* .img-container {
  width: 400px;
  height: 400px;
} */

.img {
  width: 400px;
  height: 400px;
  animation: spin 4s infinite;
}
@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  50% {
    transform: rotate(180deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>