<template lang="">
    <v-container>
        <v-row>
            <v-col cols="12" class="mx-auto">
                <v-img :src="result.current.condition.icon" height="120" width="120" class="mx-auto"></v-img>
            </v-col>
            <v-col cols="12" v-if="result" class="d-flex mx-auto flex-column"> 
                <p :class="getCelciusColor"> {{result.current.temp_c}}°C</p>   
                <p class="text-h5 blue-grey--text font-weight-medium text-center">{{city}} - {{result.location.country}}</p>
                <p class="blue--text text--lighten-1 text-center"> Current Weather: {{result.current.condition.text}}</p>
            </v-col>

            
        </v-row>
    </v-container>
    
</template>
<script>
import axios from 'axios'
import { bus } from '../main'
export default {
    data() {
        return {
            weatherApiKey: "4a30490d15c5418186e94845222307",
            baseUrl: "http://api.weatherapi.com/v1/current.json?",
            city: "",
            result: ""            
        }
    },
    computed: {
        getCelciusColor() {
            const color = this.result.current.temp_c
            let css

            if(color <= 20) css = 'text-h4 blue--text text--darken-1 font-weight-bold text-center'
            else if(color >= 20) css = 'text-h4 blue--text text--lighten-1 font-weight-bold text-center'
            else if(color >= 35) css = 'text-h4 error--text text--lighten-1 font-weight-bold text-center'      
        
            return css
        }
    },
    methods: {
        getResult() {
            axios.get(`http://api.weatherapi.com/v1/current.json?key=${this.weatherApiKey}&q=${this.city}&aqi=no`).then((response)=>{
                this.result = response.data
                // console.log(response.data)
            })
        }
    },
    created (){
        bus.$on('city', (selectedCity) => {
           this.city = selectedCity;
           this.getResult()
        })
    }
}
</script>
<style lang="">
    
</style>