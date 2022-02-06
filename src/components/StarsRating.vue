<template>
  <span class="stars">
    <i v-for="(star, i) in stars" :key="i" class="bi bi-star-fill"></i>
  </span>
</template>

<script>
export default {
  props: {
    rate: Number
  },
  computed: {
    stars () {
      return Math.ceil(this.rate / 2)
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~bootstrap-icons/font/bootstrap-icons.css';

i {
  color: yellow;
  width: 1rem;
}
</style>