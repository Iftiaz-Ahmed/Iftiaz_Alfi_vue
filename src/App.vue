<template>
  <input class="searchBar" type="text" v-model="city" placeholder="City" />
  <h1>{{ city }}</h1>
  <CurrentWeather :city=city @inputChange="checkData" />
  
</template> 

<script>
import CurrentWeather from './components/CurrentWeather.vue';

export default {
  name: 'App',
  components: {
    CurrentWeather
  },
  data() {
    return {
      city: "West Haven",
    }
  },
  methods: {

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.searchBar{
  width: 25rem;
    height: 35px;
    font-size: 25px;
    border-radius: 15px;
    padding: 8px;
}
</style>
