<template>
  <div class="card">
    CARD
    <button @click="asyncData">AsyncData</button>
  </div>
</template>

<script>
export default {
  data: () => {
    return {};
  },
  methods: {
    async asyncData() {
      const data = await this.$axios.$get(
        "https://superheroapi.com/api/2567746080028499/70/powerstats"
      );
      console.log(data);
      return { ip };
    },
  },
  name: "Card",
};
</script>

<style>
@media screen and(max-width: 400px) {
  .card {
    width: 80%;
    height: auto;
    border: solid 2px grey;
    margin: 5px;
  }
}
.card {
  width: 180px;
  height: 250px;
  border: solid 2px grey;
  margin: 5px;
}
</style>