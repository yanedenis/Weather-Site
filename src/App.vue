<script>
import axios from 'axios'
import CountryWeather from './components/CountryWeather.vue'

export default {
  components: { CountryWeather },
  data() {
    return {
      city: '',
      error: '',
      info: null,
    }
  },
  methods: {
    findWeather() {
      if(this.city.trim().length < 2) {
        this.error = 'Need more than 1 symbol'
        return false
      }
      this.error = ''

      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=9ece9e076cec8a1d100ea36ca0e7b886
`)
        .then(res => {this.info = res.data})
    }
  }
}
</script>

<template>
  <div class="wrapper">
    <h1>Weather app</h1>
    <p>Find out the weather in your country</p>
    <div class="search-bar">
        <input type="text" placeholder="Find your country" v-model="city">
        <button v-if="city != ''" @click="findWeather()">Find</button>
        <button v-else disabled title="Type your country in input">Find</button>
    </div>
    <p className="error">{{ error }}</p>
    <CountryWeather :info="info" :city="city"/>
  </div>
</template>

<style scoped>
.wrapper {
  background: rgba(255, 255, 255, .3);
  border: 1px solid rgba(255, 255, 255, .7);
  backdrop-filter: blur(10px);
  color: white;
  height: fit-content;
  padding: 20px;
  text-align: center;
  border-radius: 32px;
}

p {
  margin-top: 6px;
}

.error {
  color: black;
}

.search-bar {
  display: grid;
  grid-auto-flow: column;
  gap: 12px;
  margin: 14px 0;
}

input {
  padding: 6px 8px;
  outline: 0;
  border: 0;
  border-bottom: 2px solid #0093E9;
  font-size: 18px;
}

input::placeholder {
  color: rgba(255, 255, 255, .8);
}

button {
  background-color: #0093E9;
  padding: 8px 20px;
  border: 0;
  border-radius: 12px;
  font-size: 18px;
  color: white;
  cursor: pointer;
  transition: all .2s ease-in;
}

button:disabled {
  cursor: not-allowed;
  background-color: gray;
}

button:not(:disabled):hover {
  box-shadow: 0 0 10px 1px #0093E9;
}
</style>
