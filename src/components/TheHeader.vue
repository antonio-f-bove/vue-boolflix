<template>
  <header class="container">
    <div class="row py-3">
      <div class="logo-container col">
        <!-- super-custom logo, troveró un modo migliore di farlo ! -->
        <h1 class="d-flex align-items-center fw-bold">
          B<span class="fs-2">O</span><span class="fs-3">O</span><span class="fs-4">L</span><span class="fs-3">FL</span><span class="fs-2">I</span>X
        </h1>
      </div>
      <div class="search-bar col-3">
        <div class="row">
          <input
            v-model="searchInput"
            @keyup.enter="sendSearchResult"
            type="text"
            class="col rounded"
            placeholder="Search"
          />
          <div @click="sendSearchResult" class="search-button col ms-3 rounded py-1">Search</div>
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
@import '../style/variables.scss';

.row {
  justify-content: space-between;
}

.logo-container {
  h1 {
    color: $boolflix-red;
  }
}

.search-bar {
  .row {
    align-items: center;
    height: 100%;
  }

  input {
    border: 3px solid $boolflix-red;
    background-color: #333;
    &::placeholder {
      color: #ccc;
    }
  }
  
  .search-button {
    flex-grow: 0;
    background-color: $boolflix-red;
    color: #aaa;
    border: 1px solid $boolflix-red;
  }
}
</style>
