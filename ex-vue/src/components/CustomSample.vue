<template>
  <li class="card">
    <div class="card-header">
      <h3>Stock code: {{ dataset.stockcode }}</h3>
    </div>
    <div class="card-content">
      <p>
        <strong>Description: {{ dataset.description }}</strong>
      </p>
      <p>
        <strong>Quantity: {{ dataset.quantity }}</strong>
      </p>
      <p>
        <strong>Price: {{ dataset.price }}</strong>
      </p>
      <p>
        <strong>Invoice date: {{ dataset.invoiceDate }}</strong>
      </p>
      <p>
        <strong>Country: {{ dataset.country }}</strong>
      </p>
    </div>
  </li>
</template>

<script>
export default {
  props: {
    dataset: Object, // Define prop for dataset object
  },
};
</script>

<style scoped>
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
