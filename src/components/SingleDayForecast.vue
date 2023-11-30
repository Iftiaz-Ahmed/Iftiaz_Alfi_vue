<template>
    <div class="box">
        <p>Image</p>
        <p>Hi/Lo Temp</p>
        <p>Humidity</p>
        <p>Wind</p>
    </div>
</template>

<script>

export default{
    name: 'SingleDayForecast',
    props: {
        data: Array,
    },
    data(){
        return {
            elements: 0,
        }
    },
    methods: {

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
    }
</style>