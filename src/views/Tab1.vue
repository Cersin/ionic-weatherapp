<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Tab 1</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 1</ion-title>
        </ion-toolbar>
      </ion-header>
      <current-weather :icon="weatherIcon"></current-weather>
      <p>{{ weatherData.weather }}</p>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import axios from "axios";
import CurrentWeather from "@/components/CurrentWeather";

export default {
  name: 'Tab1',
  components: {CurrentWeather, IonHeader, IonToolbar, IonTitle, IonContent, IonPage},
  beforeMount() {
    this.getWeather();
  },
  data() {
    return {
      weatherData: {},
      weatherIcon: "",
      weatherDescription: {}
    }
  },
  methods: {
    getWeather() {
      axios.get('http://api.openweathermap.org/data/2.5/weather?q=Warszawa&appid=7ded97f2e0ce975b4a0bc4630332feec')
          .then((res) => {
            this.weatherData = res.data;
            this.weatherIcon = res.data.weather[0].icon;
            console.log(this.weatherData);
          })
    }
  }
}

</script>

<style scoped>

</style>

