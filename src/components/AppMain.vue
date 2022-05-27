<template>
  <main>
    <h1>Films</h1>
    <div class="cards-container">
      <AppCard
        v-for="(element, index) in movieList"
        :key="index"
        :movieCard="element"
      />
    </div>
    <h1>Serie TV</h1>
    <div class="cards-container">
      <AppCard
        v-for="(element, index) in seriesList"
        :key="index"
        :movieCard="element"
      />
    </div>
  </main>
</template>

<script>
import AppCard from "./AppCard.vue";
export default {
  name: "AppMain",
  props: {
    movieList: Array,
    seriesList: Array,
  },
  components: {
    AppCard,
  },
};
</script>

<style lang="scss" scoped>
$text-color: #727873;
.cards-container {
  width: 90%;
  margin: auto;
  padding-bottom: 1rem;
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
}
h1 {
  color: $text-color;
  font-size: 1.8rem;
  margin: 1rem 2.5rem;
}
</style>
