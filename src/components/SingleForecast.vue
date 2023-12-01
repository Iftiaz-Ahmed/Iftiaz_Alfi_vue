<template>
    <div class="box">
        <img :src=generateImgUrl() alt="icon">
        <p class="title">{{ data['weather'][0]['description'].toUpperCase() }}</p>
        <h1 class="temp">{{ kelvinToCelsius(data['main']['temp']) }}°</h1>
        <p style="font-size: 14px;">Wind gust of {{ data['wind']['gust'] }} mps</p>
        <p>{{formatDateString(data['dt_txt'])}}</p>
    </div>
</template>

<script>

export default{
    name: 'SingleForecast',
    props: {
        data: Object,
    },
    data(){
        return {
         
        }
    },
    methods: {
        formatDateString(inputString) {
            const inputDate = new Date(inputString);

            const options = { month: 'short', day: 'numeric', hour: 'numeric', minute: 'numeric', hour12: true };

            const formattedDate = inputDate.toLocaleString('en-US', options);

            return formattedDate;
        },
        generateImgUrl() {
            if (this.data != null) {
                const imgUrl = "https://openweathermap.org/img/wn/" + this.data['weather'][0]['icon'] + '@2x.png'

                return imgUrl
            }
        },
        kelvinToCelsius(temp) {
            return (temp - 273.15).toFixed(0)
        }
    },
    watch: {
        city: 'generateImgUrl',
    }
}

</script>

<style scoped>
    .box{
        flex: 1;
        background: var(--primary-color);
        margin: 5px;
        padding: 10px;
        text-align: center;
        letter-spacing: 0px;
        font-size: 15px;
        width: 500px;
    }

    .title{
        margin: 0px;
        font-size: 15px;
    }
    .temp{
        margin-bottom: 0px;
    }
</style>