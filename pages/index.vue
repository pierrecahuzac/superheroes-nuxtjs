<template>
  <div class="card-container">
    <Card />
    <Card /><Card /><Card /> <Card /><Card /> <Card /> <Card /><Card />
    <Card /><Card /><Card />
    <Card />
    <Card /><Card /><Card />
  </div>
</template>

<script>
import Card from "@/components/Card.vue";
export default {
  name: "IndexPage",
};
</script>
<style>
.card-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  width: 100%;
  min-height: 100vh;
}
</style>
