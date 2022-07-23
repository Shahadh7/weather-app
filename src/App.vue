<template>
  <v-app>
    
    <v-app-bar
      app
      color="primary"
    >
      <v-container class="fill-height">
          <p class="text-h5 font-weight-medium white--text ">Weather App</p>
      </v-container>
    </v-app-bar>
    <v-main class="bg d-flex justify-center" >
      <v-card
      class="mx-auto mt-5"
      elevation="5"
      width="800"
      height="600"
      
      >
        <v-col cols="12" class="ml-4 mt-5">
            <h2 class="text-lg-h5 my-3 text-sm-h5 text-md-h5 justify-sm-center blue-grey--text text--lighten-1 ">Find current weather in Sri Lanka by city.</h2>
        </v-col>
          <DropDown/>
          <WeatherResult/>
      </v-card>
      
    </v-main>
  </v-app>
</template>

<script>
import DropDown from './components/DropDown';
import WeatherResult from './components/WeatherResult';

export default {
  name: 'App',

  components: {
    DropDown,
    WeatherResult
  },
};
</script>

<style scoped>
.bg {
  background-color: #ffffff;
}
</style>
