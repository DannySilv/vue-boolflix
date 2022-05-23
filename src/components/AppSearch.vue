<template>
  <div class="search-container">
    <input
      type="text"
      placeholder="Cerca un Film o una Serie"
      v-model="thisSearch"
      @keyup.enter="$emit('searchClick', thisSearch)"
    />
    <button class="btn" @click="$emit('searchClick', thisSearch)">
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
  data: function () {
    return {
      thisSearch: "",
    };
  },
  methods: {
    resetClick() {
      this.thisSearch = "";
      this.$emit("resetClick");
    },
  },
};
</script>

<style lang="scss" scoped>
.search-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  input {
    font-family: "Ubuntu", sans-serif;
    font-size: 0.8rem;
    padding: 0.4rem 0.6rem;
    border: 1px solid white;
    border-radius: 5px;
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
