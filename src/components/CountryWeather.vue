<script>
export default {
    props: {
        info: {
            type: Object,
            required: true,
        },
        city: {
            type: Text,
            required: true,
        }
    },
    computed: {
        cityWeatherName() {
            return this.info.weather[0].main
        },
        showTemp() {
            return 'Temperature ' + Math.round(this.info.main.temp) + '°C'
        },
        showFeelsLike() {
            return 'Feels like ' + Math.round(this.info.main.feels_like) + '°C'
        },
        showMinTemp() {
            return 'Min temperature ' + Math.round(this.info.main.temp_min) + '°C'
        },
        showMaxTemp() {
            return 'Max temperature ' + Math.round(this.info.main.temp_max) + '°C'
        },
        cityName() {
            return this.info.name
        }
    }
}
</script>

<template>
    <div v-if="info != null" className="cityInfo">
        <div className="city-weather">
            <h1>{{ cityName }}</h1>
            <i class='bx bx-water' v-if="cityWeatherName == 'Mist'"></i>
            <i class='bx bxs-droplet' style="color: #00B4D8;" v-else-if="cityWeatherName == 'Rain'"></i>
            <i class='bx bxs-cloud' v-else-if="cityWeatherName == 'Clouds'"></i>
            <i class='bx bxs-sun' style="color: goldenrod;" v-else-if="cityWeatherName == 'Clear'"></i>
            <i class='bx bxs-bolt' style="color: gold;" v-else-if="cityWeatherName == 'Thunderstorm'"></i>
            <i class='bx bx-cloud-drizzle' v-else-if="cityWeatherName == 'Drizzle'"></i>
            <i class='bx bx-cloud-snow' style="color: #90E0EF;"v-else-if="cityWeatherName == 'Snow'"></i>
            <h2>{{ cityWeatherName }}</h2>
        </div>
        <div className="temps">
            <p><i class='bx bxs-thermometer'></i>{{ showTemp }}</p>
            <p><i class='bx bx-body'></i>{{ showFeelsLike }}</p>
            <p><i class='bx bxs-sun' ></i>{{ showMaxTemp }}</p>
            <p><i class='bx bxs-moon' ></i>{{ showMinTemp }}</p>
        </div>
    </div>
</template>

<style scoped>
.city-weather {
    text-transform: capitalize;
}
.cityInfo {
    display: grid;
    grid-template-columns: auto 1fr;
    height: 20vh;
    gap: 12px;
    margin-top: 24px;
    justify-items: center;
}
.city-weather i {
    font-size: 80px;
    color: lightgrey;
}
.cityInfo > div {
    background-color: rgba(255, 255, 255);
    opacity: .8;
    color: black;
    padding: 16px;
    border-radius: 24px;
    display: grid;
    align-items: center;
    width: max-content;
}
.temps > p {
    font-size: 16px;
}
.temps i {
    font-size: 30px;
    display: flex;
    justify-content: center;
    margin-bottom: 2px;
}
h2 {
    color: gray;
}
p {
    font-weight: bold;
}
</style>