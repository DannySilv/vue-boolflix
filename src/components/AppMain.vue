<template>
  <div>
    <header>
      <div class="header-container">
        <h2>BOOLFLIX</h2>
        <div class="search">
          <AppSearch
            @searchClick="genSearchResult($event)"
            @resetClick="resetSearch($event)"
          />
        </div>
      </div>
    </header>
    <div class="cards-container">
      <AppCard
        v-for="(element, index) in movieList"
        :key="index"
        :movieCard="element"
      />
    </div>
  </div>
</template>

<script>
import AppSearch from "./AppSearch.vue";
import AppCard from "./AppCard.vue";
import axios from "axios";

export default {
  name: "AppHeader",
  props: {},
  components: {
    AppSearch,
    AppCard,
  },
  data() {
    return {
      movieList: [],
    };
  },
  methods: {
    thisSearch(url, searchKey) {
      axios
        .get(url, {
          params: {
            api_key: "036d8909f87005de49ae4df23607af26",
            lang: "en-US",
            page: 1,
            query: searchKey,
          },
        })
        .then((resp) => {
          this.movieList = this.movieList.concat(resp.data.results);
        });
    },
    genSearchResult(searchKey) {
      this.thisSearch("https://api.themoviedb.org/3/search/movie", searchKey);
      this.thisSearch("https://api.themoviedb.org/3/search/tv", searchKey);
      console.log(this.movieList);
    },
    resetSearch() {
      this.movieList = [];
    },
  },
};
</script>

<style lang="scss" scoped>
$header-card-bg: #2e3a46;
$main-bg: #1e2d3b;
$text-color: #727873;

header {
  width: 100%;
  height: 80px;
  background-color: $header-card-bg;
  .header-container {
    width: 90%;
    height: 80px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  h2 {
    color: red;
  }
}
.cards-container {
  width: 90%;
  margin: 1rem auto;
  padding-bottom: 1rem;
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
}
</style>
