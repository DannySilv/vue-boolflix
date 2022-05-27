<template>
  <header>
    <div class="header-container">
      <div class="logo-container">
        <h2>BOOLFLIX</h2>
        <font-awesome-icon
          class="icon"
          icon="fas fa-chevron-down"
          @click="toggle()"
        />
      </div>
      <div class="search-container" v-if="showSearch">
        <select
          @change="$emit('filterGenre', filterGenre)"
          v-model="filterGenre"
          class="filter"
          name="filter"
          id="filter"
        >
          <option value="" selected>Filtro</option>
          <option
            v-for="element in genresList"
            :key="element.id"
            :value="element.id"
          >
            {{ element.name }}
          </option>
        </select>
        <input
          type="text"
          placeholder="Cerca un Film o una Serie"
          v-model="searchKey"
          @keyup.enter="sendSearch(), filterGenre"
        />
        <button class="btn abs-1" @click="sendSearch(), filterGenre">
          <font-awesome-icon icon="fas fa-search" />
        </button>
        <button class="btn abs-2" @click="resetClick">
          <font-awesome-icon icon="fas fa-redo" />
        </button>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: "AppHeader",
  props: {
    genresList: Array,
  },
  data: function () {
    return {
      searchKey: "",
      filterGenre: "",
      showSearch: false,
    };
  },
  methods: {
    resetClick() {
      this.thisSearch = "";
      this.$emit("resetClick");
    },
    sendSearch() {
      this.$emit("searchClick", this.searchKey);
      this.showSearch = false;
    },
    toggle() {
      if (this.showSearch == false) {
        this.showSearch = true;
      } else if (this.showSearch == true) {
        this.showSearch = false;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
$header-card-bg: #2e3a46;
$text-color: #727873;

header {
  width: 100%;
  height: 80px;
  background-color: black;
  .header-container {
    width: 100%;
    height: 80px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: relative;
  }
  .logo-container {
    position: absolute;
    top: 30%;
    left: 40px;
    width: 190px;
    display: flex;
    align-items: center;
    h2 {
      font-family: verdana;
      font-size: 1.6rem;
      font-weight: 700;
      color: red;
      text-shadow: 0px 0px 0px #930404, 1px 1px 1px #930404,
        1px 1.5px 1px #930404, 1px 2px 1px #930404, 1px 2.5px 1px #930404,
        1px 3px 1px #930404, 1px 3.5px 1px #930404, 1px 4px 1px #930404,
        1px 4.5px 1px #930404, 1px 5px 1px #930404,
        1px 18px 6px rgb(16 16 16 / 40%), 1px 22px 10px rgb(16 16 16 / 20%),
        1px 25px 35px rgb(16 16 16 / 20%), 1px 30px 60px rgb(16 16 16 / 40%);
    }
    .icon {
      font-size: 1rem;
      color: white;
      margin-left: 1rem;
      cursor: pointer;
    }
  }
}

.search-container {
  display: flex;
  width: 80%;
  margin-left: 15%;
  justify-content: flex-end;
  align-items: center;
  position: relative;
  select::-webkit-scrollbar {
    width: 0.5em;
    height: 1rem;
  }
  select::-webkit-scrollbar-track {
    box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.3);
  }
  select::-webkit-scrollbar-thumb {
    background-color: $text-color;
    outline: 1px solid white;
    border-radius: 10px;
  }
  .filter {
    position: absolute;
    width: 100px;
    top: 16%;
    right: 9%;
    font-family: "Ubuntu", sans-serif;
    font-size: 0.8rem;
    padding: 0.1rem 0;
    border: 1px solid white;
    border-radius: 5px;
    text-align: end;
    cursor: pointer;
  }
  input {
    font-family: "Ubuntu", sans-serif;
    font-size: 0.8rem;
    width: 70%;
    padding: 0.4rem 0.6rem;
    border: 1px solid white;
    border-radius: 5px;
  }
  .btn {
    position: absolute;
    padding: 0 0.2rem;
    background-color: white;
    border: 1px solid white;
    border-radius: 5px;
    cursor: pointer;
  }
  .abs-1 {
    top: 23%;
    right: 5%;
  }
  .abs-2 {
    top: 23%;
    right: 1.2%;
  }
}
</style>
