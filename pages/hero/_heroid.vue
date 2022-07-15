<template>
  <div class="heroPage" v-if="result">
    <NuxtLink class="button" :to="{ name: 'index' }"> Back </NuxtLink>
    <div>Hero Page :</div>
    <article class="card" data-aos="flip-right">
      <div class="image">
        <img class="profil" :src="`${hero}`" alt="profil" />
        <div>{{ hero.work.occupation }}</div>
        <img class="profil" :src="`${hero}`" alt="profil" />
      </div>
    </article>
  </div>
</template>

<script>
import AOS from "aos";
import "aos/dist/aos.css";
export default {
  name: "hero",
  async fetch() {
    await this.getOneHero();
  },
  data() {
    return {
      hero: "",
    };
  },
  created() {
    AOS.init();
    this.getOneHero();
  },
  mounted() {},

  methods: {
    async getOneHero() {
      const data = this.$axios.$get(
        `https://akabab.github.io/superhero-api/api/id/${this.$route.params.id}.json`
        /* `https://akabab.github.io/superhero-api/api/id/${{ characterId }}.json` */
      );
      const result = await data;
      this.hero = result;
      console.log(this.hero);
    },
    fecth() {},
  },
};
</script>  

<style>
.heroPage {
  width: 100%;
  min-height: 100vh;
}
</style>