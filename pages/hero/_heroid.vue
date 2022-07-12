<template>
  <div class="heroPage">
    <div>Hero Page :</div>
    <article class="card" data-aos="flip-right">
      <div class="image">
        <img class="profil" :src="`${hero.images.lg}`" alt="profil" />
      </div>
    </article>
  </div>
</template>

<script>
import AOS from "aos";
import "aos/dist/aos.css";
export default {
  name: "hero",
  data() {
    return {
      hero: [],
    };
  },
  created() {
    AOS.init();
    this.asyncData();
  },
  mounted() {},

  methods: {
    async asyncData() {
      const data = this.$axios.$get(
        "https://akabab.github.io/superhero-api/api/id/1.json"
      );
      const result = await data;
      console.log(result);

      /*       result.data.forEach((hero) => {
        console.log(hero); */
      this.hero.push(result.data);
      console.log(this.hero);
    },
  },
};
</script>


    

<style>
</style>