<template>
    <div class="forecast glass">
        <p>3 Hour Weather Forecast</p>
        <div v-if="forecastList.length != 0" class="parentBox">
            <SingleForecast :data=x v-for="x in forecastList" :key="x" :isCelsius=isCelsius />
        </div>
        <div v-else class="message">
            <h3>Data not available</h3>
        </div>
        
    </div>
</template>

<script>
import SingleForecast from './SingleForecast.vue';

export default{
    name: 'ThreeHourForecast',
    components: {
        SingleForecast
    },
    props: {
        city: String,
        data: Array,
        isCelsius: Boolean
    },
    data(){
        return {
            forecastList: [],
        }
    },
    methods: {
        filterData() {
            for (const element of this.data) {
                const item = element['value']
                if (item['city']['name'].toLowerCase() == this.city.toLowerCase()) {
                    this.forecastList = item['list']
                    break;
                } else {
                    this.forecastList = []
                }
            }
        },
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
    .forecast{
        padding: 20px;
    }

    .parentBox{
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
    }
    .message{
        height: 200px;
        display: flex;
        flex: 1;
        flex-direction: column;
        justify-content: center;
        text-align: center;
    }
</style>