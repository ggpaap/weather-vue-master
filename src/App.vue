<script>
export default {
  name: "app",
  data() {
    return {
      api_key: "61c42a37c6ab143f961fc730ba37cfc6",
      url_base: "https://api.openweathermap.org/dathttps://home.openweathermap.org/api_keys/2.5/",
      query: "",
      weather: {},
    };
  },
  methods: {
    fatchWeather(e) {
      if (e.key == "Enter") {
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.setResults);
      }
    },
  },
  setResults(results) {
    this.weather = results;
  },
};
</script>

<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input
          type="text"
          class="search-bar"
          placeholder="Pesquisar"
          v-model="query"
          @keypress="fetchWeather"
        />
        {{ query }}
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">
            {{ weather.name }}, {{ weather.sys.country }}
          </div>
          <div class="date">Segunda 20 de janeiro de 2022</div>
        </div>

        <div class="weather-box">
          <div class="temp">9°c</div>
          <div class="weather">Chuva</div>
        </div>
      </div>
    </main>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "Times New Roman", Times, serif;
}

#app {
  background-image: url("./assets/cold-bg.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, #00000040, #000000bf);
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  color: #000000bf;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 16px #00000040;
  background-color: #e1e1e180;
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}

.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px #00000040;
  background-color: #e1e1e180;
  border-radius: 16px 0px 16px 0px;
}

.location-box .location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px #00000040;
}

.location-box .date {
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;
  box-shadow: 3px 6px #00000040;
  background-color: #e1e1e180;
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px #00000040;
}

weather-box .weather {
  color: #fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px #00000040;
}
</style>
