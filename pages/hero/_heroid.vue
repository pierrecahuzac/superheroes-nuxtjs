<template>
  <div class="hero-info-container" v-if="hero !== ''">
    <Loading v-if="$fetchState.pending" />
    <NuxtLink class="button back-home" :to="{ name: 'index' }"> Back </NuxtLink>
    <div class="hero-container">
      <div class="hero-image">
        <img class="image" :src="`${hero.images.lg}`" alt="profil" />

        <!-- <img class="profil" :src="`${hero}`" alt="profil" /> -->
      </div>
      <div class="hero-content">
        <div>{{ hero.work.occupation }}</div>
      </div>
    </div>
  </div>
  <Loading v-else />
</template>

<script>
import AOS from "aos";
import "aos/dist/aos.css";
import Loading from "~/components/Loading.vue";

export default {
  name: "hero",
  data() {
    return {
      hero: "",
    };
  },
  async fetch() {
    /*  console.log(localStorage.setItem("test", JSON.stringify("tupeupastest"))); */
    await this.getOneHero();
    /*  console.log(localStorage.getItem("test")); */
    return;
  },
  created() {
    /*  AOS.init(); */
  },
  methods: {
    async getOneHero() {
      const data = this.$axios.$get(
        /* `https://akabab.github.io/superhero-api/api/id/${this.$route.params.id}.json` */
        `https://akabab.github.io/superhero-api/api/id/1.json`
      );
      const result = await data;
      this.hero = result;
      console.log(this.hero);
    },
  },
  components: { Loading },
};
</script>

<style scoped>
.hero-info-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  width: 100%;
  min-height: 100vh;
}
.hero-container {
  display: flex;
  justify-content: center;
  width: 100%;
  height: 100%;

  padding: 32px 16px;
}
.hero-content {
  display: flex;
  padding: 50px;
  font-size: 18px;
  color: white;
  flex-direction: column;
  box-sizing: border-box;
}
.hero-image {
}
.image {
  width: 100%;
  max-height: 700px;
}
.button {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 120px;
  height: 55px;
  border: solid 2px red;
  border-radius: 5px;
  color: white;
  background-color: red;
  text-decoration: none;
  font-weight: bold;
}
.button:hover {
  background-color: white;
  color: red;
  transition: 0.8s;
  font-weight: bold;
}
</style>
