<template>
  <header class="container">
    <div class="row">
      <div class="logo-container col">
        <h1>BOOLFLIX</h1>
      </div>
      <div class="search-bar col">
        <div class="row">
          <input
            v-model="searchInput"
            @keyup.enter="sendSearchResult"
            type="text"
            class="col"
            placeholder="Search"
          />
          <div @click="sendSearchResult" class="search-button col">Search</div>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  data() {
    return {
      searchInput: "",
    };
  },
  methods: {
    sendSearchResult() {
      this.$emit("search", this.searchInput);
      this.searchInput = "";
    },
  },
};
</script>

<style lang="scss" scoped>
.row {
  justify-content: space-between;
}
</style>
