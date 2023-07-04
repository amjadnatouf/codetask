<template>
  <div class="container">
    <h2 class="header">Our creative team</h2>
    <div class="user">
      <user v-for="user in users" :key="user.id" :user="user" />
    </div>
    <div class="controls">
      <button class="btn" @click="previousPage" :disabled="isFirstPage">
        Previous
      </button>
      <button
        v-for="pageNumber in pageNumbers"
        :key="pageNumber"
        class="btn"
        :class="{ active: pageNumber === currentPage }"
        @click="goToPage(pageNumber)"
        :disabled="pageNumber === currentPage"
      >
        {{ pageNumber }}
      </button>
      <button class="btn" @click="nextPage" :disabled="isLastPage">Next</button>
    </div>
  </div>
</template>

<script>
import user from "./components/UserCard.vue";

export default {
  components: {
    user,
  },
  data() {
    return {
      users: [],
      currentPage: 1,
      itemsPerPage: 6,
      total: 0,
      totalPages: 0,
    };
  },
  computed: {
    pageNumbers() {
      return Array.from({ length: this.totalPages }, (_, index) => index + 1);
    },
    isFirstPage() {
      return this.currentPage === 1;
    },
    isLastPage() {
      return this.currentPage === this.totalPages;
    },
  },
  methods: {
    async fetchusers() {
      let url = "https://reqres.in/api/users";
      if (this.currentPage > 1) url = url + `?page=${this.currentPage}`;

      const res = await fetch(url);
      const { data, page, per_page, total, total_pages } = await res.json();
      this.users = data;
      this.currentPage = page;
      this.itemsPerPage = per_page;
      this.total = total;
      this.totalPages = total_pages;
    },

    previousPage() {
      if (!this.isFirstPage) {
        this.currentPage--;
        this.fetchusers();
      }
    },

    nextPage() {
      if (!this.isLastPage) {
        this.currentPage++;
        this.fetchusers();
      }
    },

    goToPage(pageNumber) {
      if (
        pageNumber >= 1 &&
        pageNumber <= this.totalPages &&
        pageNumber !== this.currentPage
      ) {
        this.currentPage = pageNumber;
        this.fetchusers();
      }
    },
  },
  created() {
    this.fetchusers();
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}

body {
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' version='1.1' xmlns:xlink='http://www.w3.org/1999/xlink' xmlns:svgjs='http://svgjs.dev/svgjs' width='1440' height='560' preserveAspectRatio='none' viewBox='0 0 1440 560'%3e%3cg mask='url(%26quot%3b%23SvgjsMask1066%26quot%3b)' fill='none'%3e%3crect width='1440' height='560' x='0' y='0' fill='url(%26quot%3b%23SvgjsLinearGradient1067%26quot%3b)'%3e%3c/rect%3e%3cpath d='M858.46 274.25 a179.49 179.49 0 1 0 358.98 0 a179.49 179.49 0 1 0 -358.98 0z' fill='rgba(28%2c 83%2c 142%2c 0.4)' class='triangle-float1'%3e%3c/path%3e%3cpath d='M454.56 60.15 a128.93 128.93 0 1 0 257.86 0 a128.93 128.93 0 1 0 -257.86 0z' fill='rgba(28%2c 83%2c 142%2c 0.4)' class='triangle-float1'%3e%3c/path%3e%3cpath d='M1179.95 546.02 a135.17 135.17 0 1 0 270.34 0 a135.17 135.17 0 1 0 -270.34 0z' fill='rgba(28%2c 83%2c 142%2c 0.4)' class='triangle-float1'%3e%3c/path%3e%3cpath d='M1105.64 277.74 a102.31 102.31 0 1 0 204.62 0 a102.31 102.31 0 1 0 -204.62 0z' fill='rgba(28%2c 83%2c 142%2c 0.4)' class='triangle-float1'%3e%3c/path%3e%3cpath d='M1275.04 504.24 a102 102 0 1 0 204 0 a102 102 0 1 0 -204 0z' fill='rgba(28%2c 83%2c 142%2c 0.4)' class='triangle-float1'%3e%3c/path%3e%3cpath d='M-22.11 88.34 a106.27 106.27 0 1 0 212.54 0 a106.27 106.27 0 1 0 -212.54 0z' fill='rgba(28%2c 83%2c 142%2c 0.4)' class='triangle-float2'%3e%3c/path%3e%3c/g%3e%3cdefs%3e%3cmask id='SvgjsMask1066'%3e%3crect width='1440' height='560' fill='white'%3e%3c/rect%3e%3c/mask%3e%3clinearGradient x1='15.28%25' y1='-39.29%25' x2='84.72%25' y2='139.29%25' gradientUnits='userSpaceOnUse' id='SvgjsLinearGradient1067'%3e%3cstop stop-color='%230e2a47' offset='0'%3e%3c/stop%3e%3cstop stop-color='%2300459e' offset='1'%3e%3c/stop%3e%3c/linearGradient%3e%3c/defs%3e%3c/svg%3e");
  background-size: cover;
  background-repeat: no-repeat;
}

.container {
  width: 80%;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  gap: 5rem;
  min-height: 100vh;
}

.header {
  font-weight: 700;
  font-size: 35px;
  margin-top: 5rem;
  color: #fff;
}

.user {
  display: flex;
  gap: 1rem;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
}

.controls {
  display: flex;
  gap: 1rem;
  margin-bottom: 5rem;
}

.btn {
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
  color: #aeaeae;
}

.active {
  text-decoration: underline;
  color: #fff;
}

@media screen and (max-width: 768px) {
  .container {
    width: 95%;
  }
}
</style>
