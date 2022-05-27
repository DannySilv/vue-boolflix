<template>
  <div class="starting-page">
    <span class="text">BOOLFLIX</span>
    <div class="container">
      <h1>Benvenuto su Boolflix!</h1>
      <h2>I tuoi Film e le tue Serie TV dove e quando vuoi</h2>
      <h3>Inizia la tua ricerca!</h3>
      <div class="search-container">
        <input
          class="input"
          type="text"
          placeholder="Cerca un Film o una Serie"
          v-model="searchKey"
          @keyup.enter="sendSearch()"
        />
        <button class="btn" @click="sendSearch()">
          <font-awesome-icon icon="fas fa-search" />
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppStartingSearch",
  data: function () {
    return {
      searchKey: "",
    };
  },
  methods: {
    sendSearch() {
      this.$emit("searchClick", this.searchKey);
      this.searchKey = "";
    },
  },
};
</script>

<style lang="scss" scoped>
$header-card-bg: #2e3a46;

.starting-page {
  width: 100%;
  height: 100vh;
  background-image: url("../assets/img/background-start.jpg");
  background-size: cover;
  background-position-x: center;
  background-position-y: bottom;
  color: white;
  .text {
    position: absolute;
    top: 15%;
    right: 50%;
    transform: translate(50%, -50%);
    font-family: verdana;
    font-size: 6rem;
    font-weight: 700;
    color: red;
    text-shadow: 1px 1px 1px #930404, 1px 2px 1px #930404, 1px 3px 1px #930404,
      1px 4px 1px #930404, 1px 5px 1px #930404, 1px 6px 1px #930404,
      1px 7px 1px #930404, 1px 8px 1px #930404, 1px 9px 1px #930404,
      1px 10px 1px #930404, 1px 18px 6px rgba(16, 16, 16, 0.4),
      1px 22px 10px rgba(16, 16, 16, 0.2), 1px 25px 35px rgba(16, 16, 16, 0.2),
      1px 30px 60px rgba(16, 16, 16, 0.4);
  }
}

.container {
  padding-top: 180px;
  display: flex;
  flex-direction: column;
  align-items: center;
  h1,
  h2,
  h3 {
    text-align: center;
    margin-bottom: 0.7rem;
  }
  .search-container {
    display: flex;
    align-items: center;
    position: relative;
    .input {
      width: 300px;
      font-family: "Ubuntu", sans-serif;
      font-size: 0.8rem;
      padding: 0.3rem 0.6rem;
      border: 1px solid white;
      border-radius: 5px;
      margin-left: 0.2rem;
    }
    .btn {
      position: absolute;
      right: 0.2rem;
      padding: 0 0.2rem;
      background-color: white;
      border: 1px solid white;
      cursor: pointer;
    }
  }
}
</style>
