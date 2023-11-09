<template>
  <div class="day">{{ day }}</div>
  <div class="time">{{ time }}</div>
</template>

<script>
const day = {
  0: "Sunday",
  1: "Monday",
  3: "Tuesday",
  4: "Wednesday",
  5: "Thursday",
  6: "Friday",
  7: "Saturday",
};

export default {
  data() {
    return {
      day: day[1],
      time: this.changeHour(),
    };
  },
  methods: {
    changeHour() {
      let date = new Date();
      setTimeout(() => {
        this.time = date.getHours() + ":" + date.getMinutes();
        this.changeHour();
      }, 1000);
    },
  },
};
</script>

<style scoped>
.day {
  margin-top: 2rem;
  font-size: 1.25rem;
}
.time {
  margin-top: 0.75rem;
  font-size: 0.85rem;
}
</style>
