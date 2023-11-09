<template>
  <section id="body">
    <div class="container">
      <div class="main-body">
        <form class="form">
          <input
            type="text"
            placeholder="Enter a city name"
            class="form-input"
            v-model="location"
            :on-keypress="setLocation"
            @keyup="enter"
          />
          <button class="btn-submit" @click="search">Search</button>
        </form>
        <Clock />
        <WeatherHeader :header="header" />
        <WeatherFooter :footer="footer" />
      </div>
    </div>
  </section>
</template>

<script>
import axios from "axios";
const VITE_API_KEY = import.meta.env.VITE_API_KEY;

import WeatherHeader from "../components/WeatherHeader.vue";
import WeatherFooter from "../components/WeatherFooter.vue";
import Clock from "../components/Clock.vue";
export default {
  name: "Wheater",
  components: {
    WeatherHeader,
    WeatherFooter,
    Clock,
  },
  data() {
    return {
      location: "",
      header: {
        city: "City",
        main: 15.6,
        weather: "Sunny",
        desc: "No cloud here",
        clouds: 0,
      },
      footer: {
        humidity: "",
        wind: "",
      },
    };
  },
  methods: {
    setLocation() {
      this.location = location;
    },
    enter(e) {
      if (e.val == "enter") {
        this.search();
      }
    },
    search(e) {
      if (this.location == "" || this.location == null) {
        alert("Please enter a city name correctlly ");
      } else {
        this.getWeather(this.location);
      }
      e.preventDefault();
    },
    async getWeather(location) {
      try {
        const response = await axios.get(
          `https://api.openweathermap.org/data/2.5/weather?q=${location}&appid=${VITE_API_KEY}`
        );

        this.header.city = this.location;
        const data = response.data;

        this.header.main = Math.ceil(data.main.feels_like - 273);
        this.header.weather = data.weather[0].main;
        this.header.desc = data.weather[0].description;
        this.header.clouds = data.clouds.all;

        this.footer.humidity = data.main.humidity;
        this.footer.wind = data.wind.speed;
      } catch (err) {
        alert("Weather weather info is not found");
      }
    },
  },
};
</script>

<style scoped>
#body {
  padding: 2rem 0;
  color: #444;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  text-align: center;
  display: flex;
  justify-content: center;
}
.container {
  width: 60%;
}

.main-body {
  background-color: #ffffff;
  padding: 3rem 1.5rem;
  border-radius: 5px;
  box-shadow: 0 0 3px #999;
}

.form {
  width: 100%;
  display: flex;
}
.form-input {
  width: 100%;
  margin-right: 0.5rem;
  padding: 0.5rem;
  font-size: 0.9rem;
  border: none;
  border-radius: 2px;
  transition: ease all 200ms;
  color: #666;
  box-shadow: 0 1px 2px #f6f6f6;
}
.form-input::placeholder {
  font-size: 0.9rem;
}

.form-input:focus {
  outline: none;
  box-shadow: 0 1px 2px #999;
}
.btn-submit {
  padding: 0 0.5rem;
  cursor: pointer;
  background-color: rgb(89, 89, 248);
  border: none;
  border-radius: 2px;
  color: white;
  transition: ease all 200ms;
}
.btn-submit:hover {
  background-color: rgb(64, 64, 211);
}
</style>
