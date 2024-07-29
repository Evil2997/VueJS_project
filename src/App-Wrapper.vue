<script>
import axios from 'axios';

export default {
    data() {
        return {
            city: "",
            error: "",
            info: null,
            API: "45d2e535af15db46f2e53a8367d8ae2e",
            full_url: "https://api.openweathermap.org/data/2.5/weather?q=Seattle&appid=45d2e535af15db46f2e53a8367d8ae2e",
        }
    },
    computed: {
        cityName() {
            return "<<" + this.city + ">>"
        }
    },
    methods:{
        getWeather() {
            if(this.city.trim().length < 2) {
                this.error = "Сообщение об ошибке"
                return false
            }
            this.error = ""
            axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${this.API}`)
                .then(res => (this.info = res))
        }
    }
}
</script>

<template>
    <div class="wrapper">
        <h1>Погодное приложение</h1>
        <p>Узнать погоду в {{ city == "" ? "вашем городе" : cityName }}</p>
        <input type="text" v-model="city" placeholder="Введите город">
        <button v-if="city != ''" @click="getWeather()">Получить погоду</button>
        <button disabled v-else>Введите название города</button>
        <p class="error">{{ error }}</p>

        <p v-show="info != null">{{ info }}</p>
    </div>
</template>

<style scoped>
.error {
    color:#ff3333
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
    margin-top: 50px;
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
