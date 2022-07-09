<template>
  <div class="home">
    <Header />
    <!-- heroes -->
    <div class="container heroes">
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
            >More informations</NuxtLink
          >
        </div>
      </article>
    </div>
    <!-- <div><button @click="this.asyncData">AsyncData</button></div> -->
  </div>
</template>

<script>
/* import Card from "@/components/Card.vue"; */
import AOS from "aos";
import "aos/dist/aos.css";

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
    };
  },
  mounted() {
    AOS.init();
    this.asyncData();
  },

  methods: {
    upperCaseName() {
      const characterNameToUpperCase = this.character.name.toUpperCase();
    },
    async asyncData() {
      const data = this.$axios.$get(
        "https://akabab.github.io/superhero-api/api/all.json"
      );
      const result = await data;

      result.forEach((hero) => {
        console.log(hero);
        this.charactersList.push(hero);
      });
    },
  },
};
</script>
<style>
.home {
  box-sizing: border-box;
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
