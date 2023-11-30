<template>
  <div class="container">
        <nav class="glass"> <h3>WeatherNow</h3> </nav>

        <div id="sidebar" class="glass"> 
          <h3>Enter the name of the city</h3>
          <input class="searchBar" type="text" v-model="city" placeholder="City" /> 
        </div>
    
        <main> 
          <CurrentWeather :city=city :data=weathers /> 
        </main>
    
        <div id="content1">Content 1</div>
        <div id="content2">Content 2</div>
        <div id="content3">Content 3</div>
    
        <footer> Footer </footer>
    </div>
  
  
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

    justPrint() {
      console.log("asdahjsd")
    },
  },
  async created(){
        this.weathers = await this.fetchCurrentWeather()
        this.justPrint()
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
    "sidebar content1 content2 content3"
    "sidebar footer footer footer"
    ;
}

nav{
    grid-area: nav;
    padding: 20px;
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

#content2{
    grid-area: content2;
}

#content3{
    grid-area: content3;
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
