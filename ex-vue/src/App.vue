<template>
  <div class="container">
    <CustomHeader />
    <CustomLogo />
    <CustomButton buttonText="Search" @click="handleButtonClick" />
    <NavBar
      ref="navbar"
      :visible="navbarVisible"
      @singleSearchClick="handleSingleSearchClick"
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
    };
  },
  methods: {
    handleButtonClick() {
      console.log("Clicked");
      this.navbarVisible = !this.navbarVisible;
      console.log("Navbar toggled to:", this.navbarVisible);
    },
    async handleSingleSearchClick(searchTerm) {
      try {
        const response = await fetch("./dataSet.json");
        if (!response.ok) {
          throw new Error("Failed to fetch data");
        }
        const data = await response.json();
        const filteredData = data.filter((item) =>
          item.description.toLowerCase().includes(searchTerm.toLowerCase())
        );
        this.searchResults = filteredData;
      } catch (error) {
        console.error("Error fetching data:", error);
      }
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
  background-color: #61dbfb;
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
