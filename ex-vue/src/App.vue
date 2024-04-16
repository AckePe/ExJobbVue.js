<template>
  <div class="container">
    <CustomHeader />
    <CustomLogo />
    <CustomButton buttonText="Click me" @click="handleButtonClick" />
    <CustomFooter />
  </div>
</template>

<script>
import CustomButton from "./components/CustomButton.vue";
import CustomLogo from "./components/CustomLogo.vue";
import CustomHeader from "./components/CustomHeader.vue";
import CustomFooter from "./components/CustomFooter.vue";

export default {
  components: {
    CustomHeader,
    CustomButton,
    CustomLogo,
    CustomFooter,
  },
  methods: {
    handleButtonClick() {
      console.log("Button clicked");
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
