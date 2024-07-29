<script>
import axios from 'axios';

export default {
    data() {
        return {
            city: "",
            error: "",
            info: null,
            API: "45d2e535af15db46f2e53a8367d8ae2e",
        }
    },
    computed: {
        cityName() {
            return "<<" + this.city + ">>";
        },
        showTemp() {
            return this.info ? `Температура: ${this.info.main.temp}°C` : "";
        },
        showFeelsLike() {
            return this.info ? `Ощущается как: ${this.info.main.feels_like}°C` : "";
        },
        showMinTemp() {
            return this.info ? `Минимальная температура: ${this.info.main.temp_min}°C` : "";
        },
        showMaxTemp() {
            return this.info ? `Максимальная температура: ${this.info.main.temp_max}°C` : "";
        },
        showPressure() {
            return this.info ? `Давление: ${this.info.main.pressure} гПа` : "";
        },
        showHumidity() {
            return this.info ? `Влажность: ${this.info.main.humidity}%` : "";
        },
        showDescription() {
            return this.info ? `Описание: ${this.info.weather[0].description}` : "";
        },
        showWindSpeed() {
            return this.info ? `Скорость ветра: ${this.info.wind.speed} м/с` : "";
        },
        showCloudiness() {
            return this.info ? `Облачность: ${this.info.clouds.all}%` : "";
        },
        showVisibility() {
            return this.info ? `Видимость: ${this.info.visibility} м` : "";
        },
        showCountry() {
            return this.info ? `Страна: ${this.info.sys.country}` : "";
        },
        showSunrise() {
            return this.info ? `Время рассвета: ${new Date(this.info.sys.sunrise * 1000).toLocaleTimeString()}` : "";
        },
        showSunset() {
            return this.info ? `Время заката: ${new Date(this.info.sys.sunset * 1000).toLocaleTimeString()}` : "";
        },
    },
    methods:{
        getWeather() {
            if(this.city.trim().length < 2) {
                this.error = "Пожалуйста, введите корректное название города"
                return false
            }
            this.error = ""
            axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${this.API}&units=metric&lang=ru`)
                .then(res => {
                    this.info = res.data;
                })
                .catch(err => {
                    this.error = "Не удалось получить данные о погоде. Попробуйте еще раз.";
                    console.error(err);
                });
        }
    }
}
</script>

<template>
    <div class="wrapper">
        <h1>Погодное приложение</h1>
        <p>Узнать погоду в {{ city == "" ? "вашем городе" : cityName }}</p>
        <div class="input-button-group">
            <input type="text" v-model="city" placeholder="Введите город">
            <button v-if="city != ''" @click="getWeather()">Получить погоду</button>
            <button disabled v-else>Введите название города</button>
        </div>
        <p class="error">{{ error }}</p>
        
        <div v-if="info != null">
            <p>{{showTemp}}</p>
            <p>{{showFeelsLike}}</p>
            <p>{{showMinTemp}}</p>
            <p>{{showMaxTemp}}</p>
            <p>{{showPressure}}</p>
            <p>{{showHumidity}}</p>
            <p>{{showDescription}}</p>
            <p>{{showWindSpeed}}</p>
            <p>{{showCloudiness}}</p>
            <p>{{showVisibility}}</p>
            <p>{{showCountry}}</p>
            <p>{{showSunrise}}</p>
            <p>{{showSunset}}</p>
        </div>
    </div>
</template>

<style scoped>
.error {
    color: #ff3333;
    margin-top: 20px;
}

.wrapper {
    width: 1000px;
    height: 800px;
    border-radius: 20px;
    padding: 40px;
    background: #1f0f24;
    text-align: center;
    color: #00ffff;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.wrapper h1 {
    margin-top: 20px;
    font-size: 2.5em;
}

.wrapper p {
    margin-top: 15px;
    font-size: 1.2em;
}

.input-button-group {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 20px;
}

.wrapper input {
    padding: 10px;
    width: 60%;
    background: transparent;
    border: 2px solid #110813;
    border-radius: 5px;
    color: #cfcfcf;
    font-size: 1em;
    transition: border-color 0.3s;
}

.wrapper input:focus {
    border-color: #6e2d7d;
    outline: none;
}

.wrapper button {
    margin-left: 10px;
    padding: 10px 20px;
    background: #6e2d7d;
    border: none;
    border-radius: 5px;
    color: #fff;
    font-size: 1.2em;
    cursor: pointer;
    transition: background 0.3s, transform 0.3s;
}

.wrapper button:hover {
    background: #9c3cb2;
    transform: scale(1.05);
}
</style>
