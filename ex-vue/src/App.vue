<template>
  <div class="container">
    <CustomHeader />
    <CustomLogo />
    <CustomButton buttonText="Search" @click="handleButtonClick" />
    <NavBar
      ref="navbar"
      :visible="navbarVisible"
      @singleSearchClick="handleSingleSearchClick"
      @measureClick="handleSearchButtonClick"
    />
    <div class="content">
      <ul class="samples">
        <CustomSample
          v-for="(item, index) in searchResults"
          :key="index"
          :dataset="item"
        />
      </ul>
    </div>
    <CustomFooter />
  </div>
</template>

<script>
const seedrandom = require("seedrandom");

import CustomButton from "./components/CustomButton.vue";
import CustomLogo from "./components/CustomLogo.vue";
import CustomHeader from "./components/CustomHeader.vue";
import CustomFooter from "./components/CustomFooter.vue";
import NavBar from "./components/NavBar.vue";
import CustomSample from "./components/CustomSample.vue";

export default {
  components: {
    CustomHeader,
    CustomButton,
    CustomLogo,
    CustomFooter,
    NavBar,
    CustomSample,
  },
  data() {
    return {
      navbarVisible: false,
      searchResults: [],
      totalLoadTime: 0,
      isMeasureClicked: false,
      searchData: [],
      seed: "", // Initialize seed as empty string
    };
  },
  methods: {
    handleButtonClick() {
      console.log("Clicked");
      this.navbarVisible = !this.navbarVisible;
      console.log("Navbar toggled to:", this.navbarVisible);
    },

    async handleSearchButtonClick() {
      console.log("Measuring");
      this.isMeasureClicked = true;
      this.totalLoadTime = 0;

      // Use the same seed for all searches within a run
      const rng = seedrandom(this.seed);

      for (let i = 0; i < 1000; i++) {
        const searchTerm = this.generateRandomSearchTerm(rng);
        console.log("Search term:", searchTerm);
        this.totalLoadTime += await this.handleSearch(searchTerm);
      }
    },
    async handleSingleSearchClick() {
      await this.handleSearch(this.searchTerm);
    },
    async handleSearch(searchTerm) {
      const startTime = performance.now();
      let filteredData = [];

      try {
        const response = await fetch("./dataSet.json");
        if (!response.ok) {
          throw new Error("Failed to fetch data");
        }
        const data = await response.json();
        filteredData = data.filter((item) =>
          item.description.toLowerCase().includes(searchTerm.toLowerCase())
        );
      } catch (error) {
        console.error("Error fetching data:", error);
      }

      const endTime = performance.now();
      const measuredLoadTime = endTime - startTime;

      this.searchResults = filteredData.slice(0, 100);

      const searchItem = { searchTerm, loadTime: measuredLoadTime };
      this.searchData.push(searchItem);

      return measuredLoadTime;
    },
    generateRandomSearchTerm(rng) {
      const alphabet = "abcdefghijklmnopqrstuvwxyz";
      let searchTerm = "";

      // Generate 5 unique random letters
      for (let i = 0; i < 5; i++) {
        let randomLetter;
        do {
          randomLetter = alphabet[Math.floor(rng() * alphabet.length)];
        } while (searchTerm.includes(randomLetter));
        searchTerm += randomLetter;
      }

      return searchTerm;
    },

    saveData() {
      if (this.isMeasureClicked && this.searchData.length === 1000) {
        const dataToSave = this.searchData.map(({ searchTerm, loadTime }) => ({
          searchTerm,
          loadTime,
        }));

        const blob = new Blob([JSON.stringify(dataToSave, null, 2)], {
          type: "application/json",
        });

        const url = URL.createObjectURL(blob);
        const link = document.createElement("a");
        link.href = url;
        link.download = "search_results.json";
        document.body.appendChild(link);
        link.click();
        URL.revokeObjectURL(url);
        document.body.removeChild(link);
      }
    },
  },
  watch: {
    searchData: {
      handler() {
        this.saveData();
      },
      deep: true,
    },
  },
};
</script>

<style scoped>
.container {
  max-width: 80rem;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4.8rem;
}
.content {
  margin-top: 20px;
}

.samples {
  list-style: none;
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 2rem;
}

.card {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 10px;
  margin-bottom: 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.card-header {
  background-color: #34495e;
  border-bottom: 1px solid #ddd;
  padding: 8px 0;
  text-align: center;
  font-weight: bold;
  border-radius: 8px 8px 0 0;
}

.card-content {
  padding: 10px;
}

.card-content p {
  margin: 5px 0;
}

.searchContent {
  max-width: 100%;
  overflow-x: auto;
}

.content {
  display: flex;
  justify-content: center; /* Center horizontally */
  align-items: center;
}
</style>

<style>
body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen",
    "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue",
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: off-white;
}

code {
  font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New",
    monospace;
}
</style>
