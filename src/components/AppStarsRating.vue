<template>
  <div>
    <span v-for="(element, index) in ratings" :key="index">
      <font-awesome-icon
        class="star"
        :class="rate > index ? 'active' : ''"
        icon="fas fa-star"
      />
    </span>
  </div>
</template>

<script>
export default {
  name: "AppStarsRating",
  props: {
    rate: Number,
  },
  data() {
    return {
      ratings: [1, 2, 3, 4, 5],
    };
  },
};
</script>

<style lang="scss" scoped>
$text-color: #727873;

.star {
  color: $text-color;
  font-size: 0.8rem;
}
.active {
  color: gold;
}
</style>
