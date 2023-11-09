<template>
  <img class="weather-icon" :src="'/src/assets/' + source" />
</template>

<script>
export default {
  props: {
    source: String,
  },
};
</script>
