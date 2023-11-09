<template>
  <div class="footer">
    <div class="humidity">Humidity : {{ footer.humidity }}</div>
    <div class="wind">Wind : {{ footer.wind }}</div>
  </div>
</template>

<script>
export default {
  props: {
    footer: Object,
  },
};
</script>

<style scoped>
.footer {
  display: grid;
  grid-template-columns: 1fr 1fr;
  margin-top: 0.75rem;
}
.humidity {
  border-right: 2px solid #777;
  padding: 0.9rem;
  text-align: right;
}
.wind {
  padding: 0.9rem;
  text-align: left;
}
</style>
