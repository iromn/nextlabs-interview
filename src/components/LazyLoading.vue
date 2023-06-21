<template>
  <div class="lazy-loading">
    <h1>Lazy Loading</h1>
    <div class="card-holder">
      <div class="card" v-for="(user, index) in users" :key="index">
        <div>
          <img :src="user.picture.medium" alt="User Avatar" /><br />
          {{ user.name.first }} {{ user.name.last }}
        </div>
      </div>
    </div>
    <div ref="loadMore" class="load-more"></div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      users: [],
      page: 1,
      resultsPerPage: 6,
      isFetching: false,
    };
  },
  async mounted() {
    await this.fetchUsers();
    window.addEventListener("scroll", this.handleScroll);
  },
  beforeUnmount() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  methods: {
    async fetchUsers() {
      if (this.isFetching) return;
      this.isFetching = true;
      const response = await axios.get(
        `https://randomuser.me/api/?page=${this.page}&results=${this.resultsPerPage}&inc=name,picture`
      );
      this.users = [...this.users, ...response.data.results];
      this.isFetching = false;
    },
    handleScroll() {
      const loadMoreEl = this.$refs.loadMore;
      const bottom =
        loadMoreEl.getBoundingClientRect().bottom - window.innerHeight;

      if (bottom <= 0) {
        this.page++;
        this.fetchUsers();
      }
    },
  },
};
</script>

<style scoped>
.load-more {
  height: 0;
}
.card-holder {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
.card {
  width: calc(50% - 12px);
  margin-bottom: 24px;
}
.lazy-loading {
  width: 30vw;
  position: relative;
  left: 50%;
  transform: translate(-50%);
}
</style>
