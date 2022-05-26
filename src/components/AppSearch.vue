<template>
  <div class="search-container">
    <select
      @change="$emit('filterGenre', filterGenre)"
      v-model="filterGenre"
      class="input"
      name="filter"
      id="filter"
    >
      <option value="" selected>Filtra per genere</option>
      <option
        v-for="element in genresList"
        :key="element.id"
        :value="element.id"
      >
        {{ element.name }}
      </option>
    </select>
    <input
      class="input"
      type="text"
      placeholder="Cerca un Film o una Serie"
      v-model="searchKey"
      @keyup.enter="sendSearch(), filterGenre"
    />
    <button class="btn" @click="sendSearch(), filterGenre">
      <font-awesome-icon icon="fas fa-search" />
    </button>
    <button class="btn" @click="resetClick">
      <font-awesome-icon icon="fas fa-redo" />
    </button>
  </div>
</template>

<script>
export default {
  name: "AppSearch",
  props: {
    genresList: Array,
  },
  data: function () {
    return {
      searchKey: "",
      filterGenre: "",
    };
  },
  methods: {
    resetClick() {
      this.thisSearch = "";
      this.$emit("resetClick");
    },
    sendSearch() {
      this.$emit("searchClick", this.searchKey);
      this.searchKey = "";
    },
  },
};
</script>

<style lang="scss" scoped>
.search-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  .input {
    font-family: "Ubuntu", sans-serif;
    font-size: 0.8rem;
    padding: 0.4rem 0.6rem;
    border: 1px solid white;
    border-radius: 5px;
    margin-left: 0.2rem;
  }
  .btn {
    padding: 0.4rem 0.6rem;
    margin-left: 0.1rem;
    background-color: white;
    border: 1px solid white;
    border-radius: 5px;
  }
}
</style>
