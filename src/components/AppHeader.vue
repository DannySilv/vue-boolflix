<template>
  <header>
    <div class="header-container">
      <h2>BOOLFLIX</h2>
      <div class="search">
        <AppSearch
          @searchClicked="genSearchResult($event)"
          @resetClicked="resetSearch($event)"
        />
      </div>
    </div>
  </header>
</template>

<script>
import AppSearch from "./AppSearch.vue";
import axios from "axios";

export default {
  name: "AppHeader",
  components: {
    AppSearch,
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
</style>
