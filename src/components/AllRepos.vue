<template>
  <AppLayout />
  <div class="repos-container">
    <span class="loader" v-if="loading"></span>
    <div class="repos" :style="{ opacity: loading ? 0.5 : 1 }" v-else>
      <h1>Favour's Repositories</h1>
      <ul>
        <li
          style="text-transform: uppercase"
          v-for="repo in paginatedRepositories"
          :key="repo.id"
        >
          <router-link
            class="links"
            :to="{ name: 'single-repo', params: { id: repo.id } }"
            >{{ repo.name }}</router-link
          >
        </li>
      </ul>
      <div class="btn-container">
        <button
          @click="currentPage--"
          :disabled="currentPage === 1"
          :class="{ disabled: currentPage === 1 }"
        >
          Prev
        </button>
        <span>Page {{ currentPage }} of {{ totalPages }}</span>
        <button
          @click="currentPage++"
          :disabled="currentPage === totalPages"
          :class="{ disabled: currentPage === totalPages }"
        >
          Next
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import AppLayout from "./AppLayout.vue";
export default {
  name: "AllRepos",
  components: {
    AppLayout,
  },
  data() {
    return {
      repositories: [],
      currentPage: 1,
      perPage: 3,
      totalPages: 0,
      loading: true,
    };
  },
  methods: {
    async fetchRepositories() {
      this.loading = true;
      try {
        await new Promise((resolve) => setTimeout(resolve, 1000));
        const response = await axios.get(
          "https://api.github.com/users/favex092/repos"
        );
        this.repositories = response.data;
        this.totalPages = Math.ceil(this.repositories.length / this.perPage);
      } catch (error) {
        console.error(error);
      } finally {
        this.loading = false;
      }
    },
  },
  computed: {
    paginatedRepositories() {
      const startIndex = (this.currentPage - 1) * this.perPage;
      const endIndex = startIndex + this.perPage;
      return this.repositories.slice(startIndex, endIndex);
    },
  },
  mounted() {
    this.fetchRepositories();
  },
};
</script>

<style>
.repos-container {
  margin: 0 -1rem -1rem 0;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.2);
}
.repos {
  width: 50%;
  margin: -3rem auto 0 auto;
  padding: 1rem;
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.2);
  opacity: 1;
  transition: opacity 0.5s ease-in-out;
  color: #504b4b;
}
.loader {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  position: relative;
  animation: rotate 1s linear infinite;
}
.loader::before,
.loader::after {
  content: "";
  box-sizing: border-box;
  position: absolute;
  inset: 0px;
  border-radius: 50%;
  border: 5px solid #a79595;
  animation: prixClipFix 2s linear infinite;
}
.loader::after {
  border-color: gold;
  animation: prixClipFix 2s linear infinite, rotate 0.5s linear infinite reverse;
  inset: 6px;
}
@keyframes rotate {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
@keyframes prixClipFix {
  0% {
    clip-path: polygon(50% 50%, 0 0, 0 0, 0 0, 0 0, 0 0);
  }
  25% {
    clip-path: polygon(50% 50%, 0 0, 100% 0, 100% 0, 100% 0, 100% 0);
  }
  50% {
    clip-path: polygon(50% 50%, 0 0, 100% 0, 100% 100%, 100% 100%, 100% 100%);
  }
  75% {
    clip-path: polygon(50% 50%, 0 0, 100% 0, 100% 100%, 0 100%, 0 100%);
  }
  100% {
    clip-path: polygon(50% 50%, 0 0, 100% 0, 100% 100%, 0 100%, 0 0);
  }
}
h1 {
  color: goldenrod;
  text-align: center;
}
ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
}
li {
  font-size: 1.2rem;
  margin: 1rem 0;
  padding: 1rem;
  border: 1px solid #ccc;
  border-radius: 10px;
}
li:hover {
  background-color: #d8bbbb;
}
.pagination {
  display: flex;
  justify-content: center;
  margin-top: 1rem;
}
.links {
  color: #504b4b;
  text-decoration: none;
  cursor: pointer;
}
.links:visited {
  color: #867c7c;
}
.btn-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 2rem 0 1.5rem 0;
}
button {
  background-color: gold;
  color: #fff;
  border: none;
  padding: 0.5rem 2rem;
  border-radius: 5px;
  margin: 0 0.5rem;
  font-size: 1.2rem;
}
button:hover {
  background-color: goldenrod;
}
.disabled {
  color: grey;
  cursor: not-allowed;
}
@media (max-width: 768px) {
  .repos {
    width: 80%;
  }
  h1 {
    font-size: 1.5rem;
  }
  li {
    font-size: 1rem;
  }
  button {
    font-size: 1rem;
  }
}
</style>
