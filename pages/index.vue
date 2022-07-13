<template>
  <div class="home">
    <Header />

    <!-- heroes -->
    <div class="container heroes" v-if="charactersList.length > 0">
      <article
        class="card"
        v-for="(character, index) in charactersList"
        :key="index"
        data-aos="flip-right"
      >
        <div class="image">
          <img class="profil" :src="`${character.images.sm}`" alt="profil" />
        </div>
        <div class="info">
          <div>{{ character.name }}</div>
          <div>{{ character.biography.alignment }}</div>
          <div>{{ character.biography.publisher }}</div>
          <!-- <div>{{ character.biography.firstAppearance }}</div> -->
          <NuxtLink
            :to="`/hero/${character.id}`"
            class="link-hero"
            :prefetch="true"
            data="data"
            >More informations</NuxtLink
          >
        </div>
      </article>
    </div>
    <div class="loading" v-else>
      <Loading />
    </div>
    <Footer text />

    <!-- <div><button @click="this.asyncData">AsyncData</button></div> -->
  </div>
</template>

<script>
import AOS from "aos";
import "aos/dist/aos.css";
import Loading from "../components/Loading.vue";
import Header from "../components/Header.vue";
import Footer from "../components/Footer.vue";

export default {
  name: "IndexPage",
  head() {
    return {
      title: `Super Heroes App`,
    };
  },
  data: () => {
    return {
      charactersList: [],
      loading: true,
      text: "test",
    };
  },
  mounted() {
    AOS.init();
    this.loading = true;
    console.log("ici", this.loading);
    this.asyncData();
    this.loading = true;
    console.log("ou la", this.loading);
  },
  methods: {
    async asyncData() {
      console.log("lal", this.loading);
      const data = this.$axios.$get(
        "https://akabab.github.io/superhero-api/api/all.json"
      );
      const result = await data;
      result.forEach((hero) => {
        this.charactersList.push(hero);
      });
    },
  },
  components: { Loading, Header },
};
</script>
<style>
.home {
  box-sizing: border-box;
  min-height: 100vh;
}
.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  width: 100%;
  min-height: 100vh;
}
/* @media screen and(max-width: 400px) {
  .card {
    width: 80%;
    height: auto;
    border: solid 2px grey;
    margin: 20px;
  }
} */
.card {
  position: relative;
  display: flex;
  flex-direction: column;
  margin: 10px;
  width: 320px;
  height: 480px;
  /* justify-content: center;

  align-items: center;
  
  border: solid 2px grey;
 */
}
/* .image {
  width: 100%;
  height: auto;
} */
.profil {
  width: 100%;
  height: auto;
}
.info {
  position: absolute;
  bottom: 0;
  left: 0;
  background-color: rgb(177, 44, 44);
  position: absolute;
  width: 100%;
  color: white;
}
.link-hero {
  text-decoration: none;
  color: white;
  font-weight: bold;
  font-size: 20px;
}
.link-hero:visited {
  text-decoration: none;
  color: white;
  font-weight: bold;
  font-size: 20px;
}
</style>
