<template>
    <p>{{ data }}</p>
    <div class="container">
        <p>Current Weather</p>
        <h4>{{ city }}</h4>
        <img class="weatherIcon" :src=imgUrl alt="">
        <p>{{ weatherDesc }}</p>
        <p class="temp">{{ temp }}°</p>
    </div>
</template>

<script>

export default {
    name: 'CurrentWeather',
    props: {
        city: String
    },
    data(){
        return {
            data: [],
            temp: 0.0,
            weatherDesc: '',
            imgUrl: '',
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
                return data;
            } catch (error) {
                console.error('Error fetching data:', error);
                throw error; 
            }
        },
        kelvinToCelsius(temp) {
            return (temp - 273.15).toPrecision(1)
        }
        
    },
    async created(){
        this.data = await this.fetchCurrentWeather();
        this.temp = this.kelvinToCelsius(this.data['main']['temp'])
        this.weatherDesc = this.data['weather'][0]['description'].toUpperCase()
        this.imgUrl = "http://openweathermap.org/img/w/" + this.data['weather'][0]['icon'] + '.png'
       
    }
}

</script>

<style scoped>
    .container{
        width: 80rem;
        height: 400px;
        background: #b6edff;
        margin-left: auto;
        margin-right: auto;
        border-radius: 15px;
        padding: 15px;
        text-align: left;
    }

    .container p{
        margin-top: 0px;
    }

    .temp{
        font-size: 60px;
    }

    .weatherIcon{
        width: 100px;
        height: 100px;
    }
</style>