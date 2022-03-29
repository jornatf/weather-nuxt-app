<template>
    <div class="card">
        <div>
            <div class="card-temperature">{{ items.current.temp_c || '-' }}°C</div>
            <div class="card-location">
                <div class="card-location-name">{{ items.location.name }}</div>
                <div class="card-location-country">{{ items.location.country }}</div>
            </div>
        </div>
        <img class="weather-card-icon" width="70" height="70"
            :src="items.current.condition.icon"
            :title="items.current.condition.text"
            :alt="items.current.condition.text"
        />
    </div>
</template>

<style scoped>
    .card {
        border-radius: 20px;
        max-width: 550px;
        width: 100%;
        height: 125px;
        padding: 0 30px;
        box-shadow: 0 10px 50px rgba(0,0,0,.2);
        display: flex;
        justify-content: space-between;
        align-items: center;
        color: #F9F9F9;
        margin: 15px 0
    }

    .card-temperature {
        font-size: 35px;
        font-weight: bold;
    }

    .card-location {
        opacity: .6;
        padding-top: 10px;
    }

    .card-location-name {
        font-size: 14px;
        text-transform: uppercase;
    }

    .card-location-country {
        font-size: 12px;
        font-weight: 200;
    }

    .card-icon {
        vertical-align: middle;
    }
</style>

<script>
export default {
    name: 'WeatherCard',
    props: {
        items: Object
    }
}
</script>