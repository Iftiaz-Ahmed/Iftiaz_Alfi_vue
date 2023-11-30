<template>
    <div class="forecast glass">
        <p>7-Day Weather Forecast</p>
        <div class="parentBox">
            <SingleDayForecast v-for="x in elements" :key="x"/>
        </div>
        
    </div>
</template>

<script>
import SingleDayForecast from './SingleDayForecast.vue';

export default{
    name: 'SevenDayForecast',
    components: {
        SingleDayForecast
    },
    props: {
        data: Array,
    },
    data(){
        return {
            elements: 7,
        }
    },
    methods: {

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
        justify-content: space-between;
    }

</style>