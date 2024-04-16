<template>
  <nav v-if="visible" class="navbar">
    <input
      type="text"
      placeholder="Search..."
      v-model="searchTerm"
      @keyup.enter="handleSearch"
    />
    <button class="navbar-btn" @click="handleSingleSearchClick">Search</button>
    <button class="navbar-btn" @click="handleSearchButtonClick">Measure</button>
  </nav>
</template>

<script>
export default {
  props: {
    visible: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      searchTerm: "",
    };
  },
  methods: {
    handleSearch() {
      // Implement search logic
    },
    handleSearchButtonClick() {
      // Implement measure logic
      this.$emit("measureClick");
    },
    handleSingleSearchClick() {
      this.$emit("singleSearchClick", this.searchTerm);
    },
  },
};
</script>

<style scoped>
.navbar {
  width: 300px; /* Set your desired fixed width */
  margin: 0 auto; /* Center horizontally */
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.navbar input[type="text"] {
  margin-right: 5px; /* Adjust as necessary */
  appearance: searchfield;
  border-radius: 6px;
  border-width: 0;
  box-shadow: rgba(50, 50, 93, 0.1) 0 0 0 1px inset,
    rgba(50, 50, 93, 0.1) 0 2px 5px 0, rgba(0, 0, 0, 0.07) 0 1px 1px 0;
  box-sizing: border-box;
  font-family: -apple-system, system-ui, "Segoe UI", Roboto, "Helvetica Neue",
    Ubuntu, sans-serif;
  height: 44px;
  line-height: 1.15;
  outline: none;
  overflow: hidden;
  padding: 0 25px;
  position: relative;
  text-align: center;
  text-transform: none;
  transform: translateZ(0);
  transition: all 0.2s, box-shadow 0.08s ease-in;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  width: 100%; /* Set width to fill the container */
}

.navbar button {
  appearance: button;
  backface-visibility: hidden;
  background-color: #3bb8ef;
  border-radius: 6px;
  border-width: 0;
  box-shadow: rgba(50, 50, 93, 0.1) 0 0 0 1px inset,
    rgba(50, 50, 93, 0.1) 0 2px 5px 0, rgba(0, 0, 0, 0.07) 0 1px 1px 0;
  box-sizing: border-box;
  color: #fff;
  cursor: pointer;
  font-family: -apple-system, system-ui, "Segoe UI", Roboto, "Helvetica Neue",
    Ubuntu, sans-serif;
  font-size: 100%;
  height: 44px;
  line-height: 1.15;
  outline: none;
  overflow: hidden;
  position: relative;
  text-align: center;
  text-transform: none;
  transform: translateZ(0);
  transition: all 0.2s, box-shadow 0.08s ease-in;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  width: 175px;
  margin-right: 5px;
}
</style>
