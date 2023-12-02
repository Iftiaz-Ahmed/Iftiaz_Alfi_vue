<template>
    <div class="container glass">
        <div v-if="weather != null" class="desc">
            <p>Current Weather</p>
            <h4>{{ city }}</h4>
            <p class="temp">{{ formatTemp(this.weather['main']['temp']) }}°</p>
            <p>Feels Like: {{ formatTemp(weather['main']['feels_like']) }}°</p>
            <p>
                Max Temp: {{ formatTemp(weather['main']['temp_max']) }}°
                  -  
                Min Temp: {{ formatTemp(weather['main']['temp_min']) }}°
            </p>
            <p>Humidity: {{ weather['main']['humidity'] }}%</p>
            <p>Pressure: {{ weather['main']['pressure'] }} hPa</p>
            <p>Wind speed: {{ weather['wind']['speed'] }} mps</p>
        </div>
        <div v-if="weather != null" class="image">
            <p>{{ formatTime(weather['dt']) }}</p>
            <img class="weatherIcon" :src=imgUrl alt="">
            <p>{{ weather['weather'][0]['description'].toUpperCase() }}</p>
        </div>
        <div v-else class="message">
            <h3>Weather Data not available</h3>
        </div>
    </div>
</template>

<script>

export default {
    name: 'CurrentWeather',
    props: {
        city: String,
        data: Array,
        isCelsius: Boolean
    },
    data(){
        return {
            weather: null, 
            weatherDesc: '',
            imgUrl: '',
        }
    },
    methods: {
        filterData() {
            for (const element of this.data) {
                const item = element['value']
                if (item['name'].toLowerCase() == this.city.toLowerCase()) {
                    this.weather = item
                    break;
                } else {
                    this.weather = null
                }
            }
            if (this.weather != null) {
                this.imgUrl = "https://openweathermap.org/img/wn/" + this.weather['weather'][0]['icon'] + '@2x.png'
            }
        },
        formatTemp(temp) {
            if (this.isCelsius)
                return (temp - 273.15).toFixed(0)
            else
                return (((temp - 273.15) * (9/5)) + 32).toFixed(0)
        },
        formatTime(unixTime) {
            const timestamp = unixTime;
            const date = new Date(timestamp * 1000);

            const options = { month: 'short', day: 'numeric' };
            const formattedDate = new Intl.DateTimeFormat('en-US', options).format(date);
            return formattedDate
        }
    },
    watch: {
        city: 'filterData',
    },
    async created(){
        this.filterData()   
    }
}

</script>

<style scoped>
    .container{
        padding: 20px;
        height: 400px;
        display: flex;
        justify-content: space-between; 
    }

    .desc{
        flex: 2;
    }

    .image{
        flex: 1;
        text-align: center;
        margin-top: 45px;
        
    }

    .container p{
        margin-top: 0px;
    }

    .temp{
        font-size: 60px;
    }

    .weatherIcon{
        width: 130px;
        height: 130px;
    }

    .message{
        display: flex;
        flex: 1;
        flex-direction: column;
        justify-content: center;
        text-align: center;
    }
</style>