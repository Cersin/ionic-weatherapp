<template>
  <ion-img :src="'http://openweathermap.org/img/wn/' + icon  + '@4x.png'"></ion-img>
<!--  <p>{{ weatherData.weather }}</p>-->
</template>

<script>
import { IonImg } from '@ionic/vue';

export default {
name: "CurrentWeather",
  components: [IonImg],
  props: ['icon']
}
</script>

<style scoped>
ion-img {
  width: 20vh;
}
</style>
