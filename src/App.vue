<template>
  <main>

    <section class="search-box">
      <h1> weather city app demo </h1>
      <input
        class="search-bar"
        type="text"
        placeholder="Search..."
        v-model="query"
        @keypress="fetchWeather"
      />
    </section>

    <section class="weather-content" v-if="typeof weather.main !== 'undefined'">
      <div class="location-info">
        <div class="location">
          {{ weather.name }}, {{ weather.sys.country }}
        </div>
        <div class="date">{{ dateBuild() }}</div>
      </div>

      <div class="weather-info">
        <div class="temp">{{ Math.round(weather.main.temp) }}°C</div>
        <div class="weather">{{ weather.weather[0].main }}</div>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  data() {
    return {
      helloWorld: "Hello World",
      api_key: "829d73db36ac8df0778b15398b5a06d1",
      url_base: "http://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },
  methods: {
    // fetching the API from openweathermap.org
    // ada dokumentasinya
    fetchWeather(e) {
      if (e.key === "Enter") {
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&appid=${this.api_key}`
        )
          .then((response) => response.json())
          .then((data) => {
            this.weather = data;
          })
          .catch((error) => console.log(error));
      }
    },
    dateBuild() {
      let d = new Date();
      let months = [
        "Januar",
        "Februar",
        "März",
        "April",
        "Mai",
        "Juni",
        "Juli",
        "August",
        "September",
        "Oktober",
        "November",
        "Dezember",
      ];
      let days = [
        "Minggu",
        "Senin",
        "Selasa",
        "Rabu",
        "Kamis",
        "Jum'at",
        "Sabtu",
      ];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day}, ${date} ${month} ${year}`;
    },
  },
};
</script>

<style lang="scss">
@use "scss/main";
</style>
