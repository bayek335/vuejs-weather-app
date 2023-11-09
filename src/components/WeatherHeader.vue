<template>
  <div class="weather-header">
    <div class="location">{{ header.city }}</div>
    <h1 class="weather-deg">{{ header.main }}°</h1>
    <div class="weather">{{ header.weather }}</div>
    <div class="weather-desc">{{ header.desc }}</div>

    <WeatherIcon v-if="header.weather == 'Rain'" source="rain.png" />
    <WeatherIcon v-else-if="header.clouds < 10" source="sunny.png" />
    <WeatherIcon v-else-if="header.clouds < 50" source="few-clouds.png" />
    <WeatherIcon v-else-if="header.clouds >= 50" source="cloudy.png" />
    <WeatherIcon v-else-if="header.clouds < 10" source="few-clouds.png" />
  </div>
</template>

<script>
import WeatherIcon from "../components/WeatherIcon.vue";

export default {
  data() {
    return {};
  },
  components: {
    WeatherIcon,
    WeatherIcon,
  },
  props: {
    header: Object,
  },
  methods: {
    setLocation() {
      this.location = location;
    },
  },
};
</script>

<style scoped>
.weather-header {
  text-transform: capitalize;
}
.location {
  font-size: 2rem;
  margin-top: 4rem;
}
.weather-deg {
  margin-top: 1rem;
  font-size: 1.75rem;
  font-weight: normal;
}
.weather {
  margin-top: 0.5rem;
}
.weather-desc {
  margin-top: 0.5rem;
}
.weather-icon {
  width: 128px;
  margin: 3rem 0;
}
</style>
