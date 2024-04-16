<template>
  <div>
    <CustomLogo />
    <CustomButton buttonText="Click me" @click="handleButtonClick" />
  </div>
</template>

<script>
import CustomButton from "./components/CustomButton.vue";
import CustomLogo from "./components/CustomLogo.vue";

export default {
  components: {
    CustomButton,
    CustomLogo,
  },
  methods: {
    handleButtonClick() {
      console.log("Button clicked");
    },
  },
};
</script>

<style scoped>
body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen",
    "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue",
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: #d6f5ff;
}

code {
  font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New",
    monospace;
}

.container {
  max-width: 80rem;
  margin: 0 auto;

  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4.8rem;
}

.header {
  align-self: stretch;
}

.header h1 {
  /* Non-accessible color */
  color: #61dbfb;
  /* color: #af8602; */

  text-transform: uppercase;
  text-align: center;
  font-size: 5.2rem;
  font-weight: 300;
  letter-spacing: 3px;
  position: relative;
  width: 100%;
  display: block;
}
</style>
