<template>
  <div class="container">
        <nav class="glass"> 
          <img src="icon.png" class="icon" alt="icon">
          <h3>WeatherNow</h3> 
        </nav>

        <div id="sidebar" class="glass"> 
          <h3>Enter the name of the city</h3>
          <input class="searchBar" type="text" v-model="city" placeholder="City" /> 
        </div>
    
        <main> 
          <CurrentWeather :city=city :data=weathers /> 
        </main>
    
        <div id="content1">
          <SevenDayForecast />
        </div>
    
        <footer> Footer </footer>
    </div>
  
  
</template> 

<script>
import CurrentWeather from './components/CurrentWeather.vue';
import SevenDayForecast from './components/SevenDayForecast.vue';

export default {
  name: 'App',
  components: {
    CurrentWeather,
    SevenDayForecast
  },
  data() {
    return {
      city: "",
      weathers: [],
    }
  },
  methods: {
    async fetchCurrentWeather() {
      try {
        const res = await fetch("https://iftiaz-alfi-node.onrender.com/api"); 
        if (!res.ok) {
          throw new Error('Network response was not ok');
        }
        const data = await res.json();
        console.log("API Response:", data); // Add this line
        return data['weathers'];
      } catch (error) {
        console.error('Error fetching data:', error);
        throw error;
      }
    },
  },
  async created(){
        this.weathers = await this.fetchCurrentWeather()
        this.city = "West Haven"
  }
}
</script>

<style>
:root{
    --main-radius: 5px;
    --main-padding: 5px;
    --primary-color: #191B1F;
    --secondary-color: #040720;
}

body{
    font-family: 'Arvo', serif;
    background: var(--primary-color);
    color: white;
}

.container{
    display: grid;
    height: 100vh;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-template-rows: 0.3fr 1.5fr 1.2fr 1.0fr;
    gap: 0.5rem;
    grid-template-areas: 
    "nav nav nav nav"
    "sidebar main main main"
    "sidebar content1 content1 content1"
    "sidebar footer footer footer"
    ;
}

nav{
    grid-area: nav;
    display: flex;
    padding: 20px;
}

.icon{
  height: 25px;
  width: 25px;
  margin-right: 10px;
}

nav h3{
  margin: 0px;
}

#sidebar{
    grid-area: sidebar;
    text-align: center;
    padding: 10px;
    letter-spacing: 2px;
    padding-top: 5rem;
}

main{
    grid-area: main;
}

#content1{
    grid-area: content1;
}

footer{
    grid-area: footer;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  letter-spacing: 2px;
}

.searchBar{
    width: 23rem;
    height: 35px;
    font-size: 20px;
    border-radius: 12px;
    padding: 8px;
}

.glass{
    background: linear-gradient(135deg, #ffffff1a, #ffffff00);
    backdrop-filter: blur(10px);
    border-radius: 20px;
    border:1px solid #ffffff2e;
    box-shadow: 0 8px 32px 0 #0000005e;
}
</style>
