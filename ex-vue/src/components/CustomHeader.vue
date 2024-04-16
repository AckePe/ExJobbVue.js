<template>
  <header class="header">
    <h1>Vue.js</h1>
  </header>
</template>

<script>
export default {
  // Component logic
};
</script>

<style scoped>
.header {
  align-self: stretch;
}

.header h1 {
  /* Non-accessible color */
  color: #34495e;

  text-transform: uppercase;
  text-align: center;
  font-size: 5.2rem;
  font-weight: 300;
  letter-spacing: 3px;
  position: relative;
  width: 100%;
  display: block;
}

.header h1::before,
.header h1::after {
  display: block;
  content: "";
  height: 3px;
  width: 4rem;
  background-color: #34495e;
  position: absolute;
  top: calc(50% - 1px);
}

.header h1::before {
  left: 0;
}

.header h1::after {
  right: 0;
}
</style>
