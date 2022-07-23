<template>
    <v-container >
    <v-row class="">
      <v-col cols="6" class="mx-auto text-sm">
        <v-combobox
          :items="cities"
          label="Select a City"
          outlined
          v-model="selectedCity"
          height="50"
          color="blue"
        ></v-combobox>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
import axios from 'axios'
import { bus } from '../main'
export default {
    name: 'DropDown',
    data() {
        return{
            cities:[],
            country : "Sri lanka",
            selectedCity: "",
            countryApi: "https://countriesnow.space/api/v0.1/"
        }
    },
    methods: {
        getAllLocations() {
            axios.post(`${this.countryApi}countries/cities`,{
                "country" : this.country
            }).then((response) => {
                let sortedArray = response.data.data.sort(function(x,y) {
                if(x < y) { return -1; }
                if(x > y) { return 1; }
                return 0;
                })
                sortedArray = sortedArray.filter(item=> !item.includes("District"))
                this.cities = sortedArray
            })
        }

    },
    mounted() {
        this.getAllLocations()
    },
    watch: {
        selectedCity: function (val) {
            if (this.selectedCity.length > 0) {
                bus.$emit('city', val);
            }
        },
    }
}
</script>

<style>
    
</style>