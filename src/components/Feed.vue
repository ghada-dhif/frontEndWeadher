/* eslint-disable */

<template>
  <div id="app">
    <main>
      <div class="weather-wrap">
        <div class="location-box">
          <div class="location">
            <p>{{ cityData.name }}</p>
          </div>
          <div class="date">
            {{ new Date().toISOString().substr(0,10)}}
          </div>
        </div>
        <div class="weather-box">
          <div class="temp">{{ cityData.main.temp || 0 }}°F</div>
          <div class="weather">{{ cityData.weather[0].main|| "clear" }}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import { io } from 'socket.io-client'

const socket = io('http://localhost:3001/', {
  reconnectionDelayMax: 10000})
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Feed',
  data () {
    return {
      msg: 'Welcome to feed',
      counter: 0,
      weather: [],
      errors: [],
      test: [],
      city: '',
      index: 0,
      cityData: {name: '', main: {temp: 0}, weather: [{main: ''}]}
    }
  },
  async mounted () {
    socket.on('news', (data) => {
      this.cityData = data
    })
  },
  methods: {
    setTheData (data) {
      this.cityData = data
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: "montserrat", sans-serif;
}
#app {
  background-image: url("../assets/background.jpeg");
  background-size: cover;
  background-position: center;
  transition: 0.4s;
}
main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.25),
    rgba(0, 0, 0, 0.75)
  );
}
.location-box .location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.location-box .date {
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
  font-style: italic;
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
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather-box .weather {
  color: #fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
