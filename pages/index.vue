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
          <!-- <img :src="`${character[index].imageURL}`" alt="image profil" /> -->
          <img class="profil" :src="`${character.images.sm}`" alt="profil" />
        </div>
        <div class="info">
          <div>{{ character.name }}</div>
          <div>{{ character.slug }}</div>
        </div>
        <button><NuxtLink to="/:id" :prefetch="true" />ok</button>
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
    async asyncData() {
      const data = this.$axios.$get(
        /* "https://api.disneyapi.dev/characters" */
        "https://akabab.github.io/superhero-api/api/all.json"
        /* {
          headers: {
            "Access-Control-Allow-Origin": "*",
            "Access-Control-Allow-Methods":
              "GET, POST, PATCH, PUT, DELETE, OPTIONS",
            "Access-Control-Allow-Headers":
              "Origin, Content-Type, X-Auth-Token",
          },
        } */
      );
      const result = await data;

      /*       console.log(result); */
      /*  console.log(result[0].biography);
      /*  console.log(this.charactersList); */
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
@media screen and(max-width: 400px) {
  .article {
    width: 80%;
    height: auto;
    border: solid 2px grey;
    margin: 20px;
  }
}
.card {
  display: flex;
  flex-direction: column;
  margin: 10px;
  /* justify-content: center;

  align-items: center;
  width: 160px;
  height: 240px;
  border: solid 2px grey;
 */
  position: relative;
} /*
.image {
  position: relative;
  top: 0;
  left: 0;
  width: 240px;
  height: 320px;
} 
.profil {
  position: absolute;
  max-width: 180px;
  height: auto;
  z-index: -1;
  overflow: hidden;
} */
/* .info {
  position: absolute;
  bottom: -10;
  left: 0;
}
.info:hover {
  position: absolute;
  bottom: 0;
  left: 0;
} */
</style>
