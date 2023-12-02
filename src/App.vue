<template>
  <div class="container">
        <nav class="glass"> 
          <div style="display: flex;">
            <img src="icon.png" class="icon" alt="icon">
            <h3>WeatherNow</h3> 
          </div>
          <button @click="toggleTemp" class="toggle">{{ isCelsius ? 'Celsius' : 'Fahrenheit' }}</button>
        </nav>

        <div id="sidebar" class="glass"> 
          <h3>Enter the name of the city</h3>
          <input class="searchBar" type="text" v-model="city" placeholder="City" />
          <div><small>E.g: West Haven, New York, San Francisco</small></div>
          
          <div class="bottom">
            <p>© All rights reserved by Iftiaz Ahmed Alfi</p>
          </div>
        </div>
    
        <main> 
          <CurrentWeather :city=city :data=weathers :isCelsius=isCelsius /> 
        </main>
    
        <div id="content1">
          <ThreeHourForecast :city=city :data=threeHourForecasts :isCelsius=isCelsius />
        </div>

        <footer class="glass">
          <p>© All rights reserved by Iftiaz Ahmed Alfi</p>
        </footer>
    </div>
  
  
</template> 

<script>
import CurrentWeather from './components/CurrentWeather.vue';
import ThreeHourForecast from './components/ThreeHourForecast.vue';

export default {
  name: 'App',
  components: {
    CurrentWeather,
    ThreeHourForecast
  },
  data() {
    return {
      city: "",
      weathers: [],
      threeHourForecasts: [],
      isCelsius: true
    }
  },
  methods: {
    async fetchCurrentWeather() {
      try {
        const res = await fetch("https://iftiaz-alfi-node.onrender.com/api/currentWeather"); 
        if (!res.ok) {
          throw new Error('Network response was not ok');
        }
        const data = await res.json();
        console.log("API Response:", data); // Add this line
        return data;
      } catch (error) {
        console.error('Error fetching data:', error);
        throw error;
      }
    },
    async fetchThreeHourForecast() {
      try {
        const res = await fetch("https://iftiaz-alfi-node.onrender.com/api/threeHourForecast"); 
        if (!res.ok) {
          throw new Error('Network response was not ok');
        }
        const data = await res.json();
        console.log("API Response:", data); // Add this line
        return data;
      } catch (error) {
        console.error('Error fetching data:', error);
        throw error;
      }
    },
    toggleTemp() {
      this.isCelsius = !this.isCelsius
    }
  },
  async created(){
        this.weathers = await this.fetchCurrentWeather()
        this.threeHourForecasts = await this.fetchThreeHourForecast()
        this.city = "West Haven"
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

:root{
    --primary-color: #191B1F;
    --secondary-color: #040720;
}

body{
    font-family: 'Roboto', sans-serif;
    background: var(--primary-color);
    color: white;
    letter-spacing: 2px;
}

.container{
    display: grid;
    height: 100vh;
    grid-template-columns: 0.5fr 2fr;
    grid-template-rows: 0.2fr 1.5fr 1.3fr;
    gap: 0.5rem;
    grid-template-areas: 
    "nav nav"
    "sidebar main"
    "sidebar content1"
    ;
}

nav{
    grid-area: nav;
    display: flex;
    padding: 20px;
    justify-content: space-between;
}

.toggle{
  padding: 5px 20px;
  border: 2px solid #ffffff2e;
  border-radius: 10px;
  letter-spacing: 2px;
  background: var(--primary-color);
  color: white;
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
  display: none;
  font-size: 14px;
  text-align: center;
}

.searchBar{
    width: 23rem;
    height: 35px;
    font-size: 20px;
    border-radius: 12px;
    padding: 8px;
}

input{
  text-align: center;
}

.glass{
    background: linear-gradient(135deg, #ffffff1a, #ffffff00);
    backdrop-filter: blur(10px);
    border-radius: 20px;
    border:1px solid #ffffff2e;
    box-shadow: 0 8px 32px 0 #0000005e;
}

small{
  font-size: 10px;
}

.bottom{
  position: absolute;
  bottom: 10px;
  left: 40px;
  font-size: 15px;
  
}

@media only screen and (max-width: 1060px) {
  .container{
    display: grid;
    height: 100vh;
    grid-template-columns: 1fr;
    grid-template-rows: 0.3fr 0.7fr 1.5fr 1.3fr 0.2fr;
    gap: 0.5rem;
    grid-template-areas: 
    "nav"
    "sidebar"
    "main"
    "content1"
    "footer"
    ;
  }

  #sidebar{
    padding-top: 1rem;
  }

  .bottom{
    display: none;
  }

  footer{
    display: block;
  }

}

</style>
