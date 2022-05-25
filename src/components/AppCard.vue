<template>
  <div class="card-container">
    <div v-if="movieCard.poster_path" class="img-container">
      <img
        :src="'https://image.tmdb.org/t/p/w342' + movieCard.poster_path"
        alt=""
      />
    </div>
    <div v-else class="flex">
      <h1>No image available</h1>
    </div>
    <div class="info-container">
      <div class="row">
        <h2>Titolo:</h2>
        <h3 class="text">{{ movieCard.title || movieCard.name }}</h3>
      </div>
      <div class="row">
        <h2>Titolo originale:</h2>
        <h3 class="text">
          {{ movieCard.original_title || movieCard.original_name }}
        </h3>
      </div>
      <div class="row-language">
        <h2>Lingua:</h2>
        <AppFlags :flagLanguage="this.movieCard.original_language" />
      </div>
      <div class="row">
        <h2>Voto:</h2>
        <AppStarsRating :rate="movieRate(this.movieCard.vote_average)" />
      </div>
      <div class="row">
        <h2>Overview:</h2>
        <p class="text">{{ movieCard.overview }}</p>
      </div>
      <div class="row">
        <h2>Cast:</h2>
        <ul>
          <li v-for="(actors, index) in castList" :key="index">
            {{ actors.original_name }}
          </li>
        </ul>
      </div>
      <div class="row">
        <h2>Genere:</h2>
        <ul>
          <li v-for="(genres, index) in genresList" :key="index">
            {{ genres.name }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import AppFlags from "./AppFlags.vue";
import AppStarsRating from "./AppStarsRating.vue";
import axios from "axios";

export default {
  name: "AppCard",
  props: {
    movieCard: Object,
  },
  components: {
    AppFlags,
    AppStarsRating,
  },
  data() {
    return {
      rate: "",
      castList: [],
      genresList: [],
    };
  },
  created() {
    const params = {
      api_key: "036d8909f87005de49ae4df23607af26",
      language: "it-IT",
    };
    const cast = axios.get(
      `https://api.themoviedb.org/3/movie/${this.movieCard.id}/credits`,
      { params }
    );
    const genre = axios.get(
      `https://api.themoviedb.org/3/movie/${this.movieCard.id}`,
      {
        params,
      }
    );
    axios.all([cast, genre]).then((resp) => {
      this.castList = resp[0].data.cast.splice(0, 5);
      this.genresList = resp[1].data.genres;
    });
  },
  methods: {
    movieRate(number) {
      this.rate = Math.ceil(number / 2);
      return this.rate;
    },
  },
};
</script>

<style lang="scss" scoped>
$header-card-bg: #2e3a46;
$main-bg: #1e2d3b;
$text-color: #727873;

.card-container {
  width: calc(100% / 4 - 15px);
  background-color: $header-card-bg;
  padding: 1.5%;
  margin: 5px 0;
  margin-left: 15px;
  &:hover {
    transform: scale(1.1, 1.1) translateY(-5px);
    opacity: 0.9;
    transition-duration: 1s;
    .img-container {
      display: none;
    }
    .flex {
      display: none;
    }
    .info-container {
      display: flex;
    }
  }
}
.info-container {
  display: none;
  flex-direction: column;
  .row {
    display: flex;
    align-items: baseline;
    flex-wrap: wrap;
    justify-content: flex-start;
    margin-top: 0.5rem;
  }
  .row-language {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    justify-content: flex-start;
    margin-top: 0.5rem;
  }
}
.flex {
  display: flex;
  align-items: center;
  height: 100%;
  h1 {
    color: $text-color;
    text-align: center;
  }
}
h2 {
  color: $text-color;
  font-size: 0.8rem;
  text-align: start;
  margin-right: 0.5rem;
}
.text {
  margin: 0;
  font-weight: 300;
  text-align: start;
  color: $text-color;
}
h3 {
  font-size: 0.8rem;
}
p {
  font-size: 0.7rem;
}
li {
  margin: 0;
  font-weight: 300;
  text-align: start;
  color: $text-color;
  font-size: 0.7rem;
}
</style>
