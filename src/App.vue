<template>
  <div id="app">
    <AppHeader
      @searchClick="thisSearch($event)"
      @resetClick="resetSearch"
      @filterGenre="thisFilter($event)"
      :genresList="genresList"
    />
    <AppMain 
      :movieList="movieList"
      :seriesList="seriesList"
    />
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    AppHeader,
    AppMain,
  },
  data() {
    return {
      apiKey: "036d8909f87005de49ae4df23607af26",
      movieList: [],
      seriesList: [],
      genresMovieList: [],
      genresSeriesList: [],
      genresList: [],
    };
  },
  methods: {
    thisSearch(searchKey) {
      const params = {
        api_key: this.apiKey,
        lang: "it-IT",
        query: searchKey,
      };
      const movies = axios.get("https://api.themoviedb.org/3/search/movie", {
        params,
      });
      const series = axios.get("https://api.themoviedb.org/3/search/tv", {
        params,
      });
      const genresMovies = axios.get(
        "https://api.themoviedb.org/3/genre/movie/list",
        {
          params,
        }
      );
      const genresSeries = axios.get(
        "https://api.themoviedb.org/3/genre/tv/list",
        {
          params,
        }
      );
      axios.all([movies, series, genresMovies, genresSeries]).then((resp) => {
        this.genresMovieList = resp[0].data.results;
        this.movieList = this.genresMovieList;
        this.genresSeriesList = resp[1].data.results;
        this.seriesList = this.genresSeriesList;
        const movieGenres = resp[2].data.genres;
        console.log(movieGenres);
        const seriesGenres = resp[3].data.genres;
        const genresMovieID = function () {
          const genresMovieIDs = [];
          movieGenres.forEach((genre) => {
            genresMovieIDs.push(genre.id);
          });
          return genresMovieIDs;
        };
        const filterSeriesGenres = seriesGenres.filter((genre) => {
          const genresMovieIDs = genresMovieID();
          if (!genresMovieIDs.includes(genre.id)) {
            return true;
          }
        });
        this.genresList = movieGenres.concat(filterSeriesGenres);
      });
    },
    resetSearch() {
      this.movieList = [];
      this.seriesList = [];
      this.genresList = [];
    },
    thisFilter(thisID) {
      if (thisID !== "") {
        this.movieList = this.genresMovieList.filter((movie) => {
          if (movie.genre_ids.length > 0) {
            for (let i = 0; i < movie.genre_ids.length; i++) {
              if (movie.genre_ids[i] == thisID) {
                return true;
              }
            }
          }
        });
      } else {
        this.movieList = this.genresMovieList;
      }
      if (thisID !== "") {
        this.seriesList = this.genresSeriesList.filter((serie) => {
          if (serie.genre_ids.length > 0) {
            for (let i = 0; i < serie.genre_ids.length; i++) {
              if (serie.genre_ids[i] == thisID) {
                return true;
              }
            }
          }
        });
      } else {
        this.seriesList = this.genresSeriesList;
      }
    },
  },
};
</script>

<style lang="scss">
@import "./style/style.scss";

#app {
  width: 100%;
  height: 100vh;
}
</style>
