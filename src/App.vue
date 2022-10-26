<template>
  <div id="app">
    <div class="main" :style="mainStyle">
      <div class="weather">
        <input
          type="text"
          class="text"
          v-model="query"
          @keypress="fetchweather($event)"
        />
        <h3 class="erae">{{ weather.name }}</h3>
        <p class="date">{{ date_function() }}</p>
        <div class="viwe-box" :style="mainStylee" >
          <h1 class="temp">{{ temp }}° </h1>
          <h2 class="main-weather">{{ mainWeather }}</h2>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      urlweather: "http://api.openweathermap.org/data/2.5/",
      keys: "874eb0013cebef8a83f5874f687044dd",
      query: "",
      weather: {},
      mainWeather: {},
      temp: {},
      mainStyle: {},
      mainStylee: {},
    };
  },
  methods: {
    fetchweather(e) {
      if (e.key == "Enter") {
        fetch(`${this.urlweather}weather?q=${this.query},&appid=${this.keys}`)
          .then((res) => {
            return res.json();
          })
          .then(this.setResults);
      }
    },

    setResults(result) {
      console.log(result);
      this.weather = result;
      var dgree = result.main.temp;
      this.temp = Math.round(dgree - 273.15);

      this.mainWeather = result.weather[0].main;
      this.imageWeather();
      this.styling()
    },
    styling(){
      this.mainStylee.display = "block" ;
    },
    imageWeather() {
      if (this.mainWeather == "Clouds") {
        this.mainStyle.background =
          "url(" + require("@/assets/clouds.jpg") + ")";
      }
      if (this.mainWeather == "Clear") {
        this.mainStyle.background =
          "url(" + require("@/assets/Clear.jpg") + ")";
      }
      if (this.mainWeather == "Thunderstorm") {
        this.mainStyle.background =
          "url(" + require("@/assets/Thunderstorm.jpg") + ")";
      }
      if (this.mainWeather == "snow") {
        this.mainStyle.background = "url(" + require("@/assets/snow.jpg") + ")";
      }
      if (this.mainWeather == "sun") {
        this.mainStyle.background = "url(" + require("@/assets/sun.jpg") + ")";
      }
      if (this.mainWeather == "Rain") {
        this.mainStyle.background = "url(" + require("@/assets/rain.jpg") + ")";
      } else {
        console.log("no");
      }
    },

    date_function: function () {
      let d = new Date();
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let date = d.getDate();
      let day = days[d.getDay()];
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  height: 100vh;
}

.main {
  background-color: #73aeca;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  height: 100%;
  position: relative;
  opacity: 0.7;
}

.weather {
  color: #fff;
  padding-top: 200px;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  height: 100%;
  position: relative;
  background-color: #00000059;
}

.text {
  width: 425px;
  height: 50px;
  border-radius: 15px 0;
  opacity: 0.7;
  border: none;
  margin-bottom: 40px;
  padding: 10px;
  font-size: 20px;
  color: rgb(76, 74, 74);
}

.text:focus {
  border-radius: 0 15px;
  outline: none;

  opacity: 0.8;
  box-shadow: 2px 5px #0000003b;
}

.erae {
  font-size: 40px;
}

.date {
  font-size: 12px;
  margin-bottom: 40px;
}
.viwe-box {
  display: none;
  background: none;
}
.temp {
  font-size: 100px;
  font-weight: bolder;
  text-shadow: 2px 5px #0000003b;
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 16%;
  background: #ffffff5c;
  border-radius: 20px;
  margin-top: 20px;
  margin-bottom: 40px;
}

.main-weather {
  font-size: 30px;
  font-weight: bolder;
  text-shadow: 2px 3px #4242426a;
}
</style>
