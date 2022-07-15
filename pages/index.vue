<template>
  <div class="home">
    <!--  <Header /> -->
    <!-- heroes -->
    <input type="text" placeholder="Search" />
    <Loading v-if="$fetchState.pending" />
    <div class="container heroes" v-else>
      <article
        class="card"
        v-for="(character, index) in charactersList"
        :key="index"
        data-aos="flip-right"
      >
        <div class="image-container">
          <img class="profil" :src="`${character.images.sm}`" alt="profil" />
        </div>
        <div class="info">
          <div>{{ character.name }}</div>
          <div>{{ character.biography.alignment }}</div>
          <div>{{ character.biography.publisher }}</div>
          <!-- <div>{{ character.biography.firstAppearance }}</div> -->
          <!-- :to="`/hero/${character.id}`"  -->
          <NuxtLink
            :to="{
              name: 'hero-heroid',
              params: { id: charactersList.id },
            }"
            class="link-hero"
            data="data"
            characterId="characterId"
            hero="charactersList"
            >More Info</NuxtLink
          >
        </div>
      </article>
    </div>
    <!-- <div class="loading"> -->

    <!-- </div> -->
    <!--  <Footer /> -->

    <!-- <div><button @click="this.asyncData">AsyncData</button></div> -->
  </div>
</template>

<script>
import AOS from "aos";
import "aos/dist/aos.css";
import Loading from "../components/Loading.vue";
import Header from "../components/Header.vue";
/* import Footer from "../components/Footer.vue"; */

export default {
  name: "IndexPage",
  head() {
    return {
      title: " Super Heroes App ",
    };
  },
  data: () => {
    return {
      charactersList: [],
      loading: false,
      text: "test",
      charactedId: "",
    };
  },
  async fetch() {
    await this.getAllCharacters();
    return;
  },
  mounted() {
    AOS.init();
    /* this.asyncData(); */
  },
  methods: {
    async getAllCharacters() {
      const data = this.$axios.$get(
        "https://akabab.github.io/superhero-api/api/all.json"
      );
      const result = await data;

      result.forEach((hero) => {
        this.charactersList.push(hero);
      });
      console.log(this.charactersList);
      this.loading = false;
    },
    async searchCharacter() {
      const data = this.$axios.$get(
        `https://akabab.github.io/superhero-api/api/${this.searchCharacter}.json`
      );
      const result = this.data;
    },
  },
  components: { Loading, Header },
};
</script>
<style scoped >
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
  /*  @media screen and (max-width: 600px) {
    width: 480px;
    height: 640px;
  } */
  position: relative;
  display: flex;
  flex-direction: column;
  margin: 10px;
  width: 320px;
  height: 480px;

  /* justify-content: center;

  align-items: center;
  
  
 */
}

.image-container {
  width: 100%;
  max-height: 100%;
}
.profil {
  width: 100%;
  height: 100%;
}

.info {
  position: absolute;
  bottom: 0;
  left: 0;
  background-color: red;
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
.link-hero:hover {
  color: blue;
  transition: 0.3s;
}
</style>
