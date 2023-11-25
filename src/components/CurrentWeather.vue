<template>
    <h2>This is the city value from Current Weather {{ city }}</h2>
    <p>{{ data }}</p>
</template>

<script>

export default {
    name: 'CurrentWeather',
    props: {
        city: String
    },
    data(){
        return {
            data: []
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
        }
    },
    async created(){
        this.data = await this.fetchCurrentWeather()
    }
}

</script>

<style scoped>

</style>