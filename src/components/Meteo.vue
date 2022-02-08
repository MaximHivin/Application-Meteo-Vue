<template>
    
    <div class="container"> 

        <h1 class="text-center fw-bold mt-5">
        {{ txt }}
        </h1>   

        <div class="form-group mb-5">
            <label for="position" class="mt-5 p-2 fw-bold">Entrez le nom d'une ville</label>
            <input 
            id="position"
            type="text"
            class="form-control"
            v-model="requete"
            v-on:keypress="goMeteo">
        </div>   

        <div class="border border-3 w-50 m-auto" v-if="temps">
            <h3 class="text-center mb-3">{{temps.name}}</h3>
            <div class="card text-center p-5">
                <p class="text-affichage">
                    Temperature: {{temps.main.temp.toFixed()}}°
                </p>
                <p class="text-affichage">
                    Temperature minimale: {{temps.main.temp_min.toFixed()}}°
                </p>
                <p class="text-affichage">
                    Temperature maximale: {{temps.main.temp_max.toFixed()}}°
                </p>
                <p class="text-affichage">
                    Ciel: {{temps.weather[0].description}}
                </p>
            </div>
        </div>

    </div>

</template>

<script>

import axios from 'axios'

export default {

    name: 'Meteo',
    data() {
        return {
            txt: 'WeatherApp.com',
            requete: '',
            temps: undefined,
            api_code: 'cacdeacebccaa820f7c84aff5f58ca6c',
            url_recherche: 'https://api.openweathermap.org/data/2.5/weather?' 
            
        }
    },
    methods: {
        goMeteo(event) {

            if(event.key == "Enter") {
                axios.get(`${this.url_recherche}q=${this.requete}&units=metric&appid=${this.api_code}&lang=fr`)
                .then(response => {
                    // console.log(response);
                    this.temps = response.data;
                    console.log(this.temps);  
                })
                this.requete = ''
               
                
            }
        }
    }
       
}

</script>

<style scoped>

    .text-affichage {
        font-size: 25px;
        font-weight: 400;
        line-height: 1.2;
    }
</style>
