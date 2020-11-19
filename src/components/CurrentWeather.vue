<template>
  <ion-card>
    <ion-card-header>
      {{ town }}, {{ sys.country }}
    </ion-card-header>
      <ion-card-subtitle>
        <slot></slot>
      </ion-card-subtitle>
    <ion-card-title>
      <ion-img :src="'https://openweathermap.org/img/wn/' + description.icon  + '@4x.png'"></ion-img>
    </ion-card-title>

    <ion-card-content>
    {{ Math.round(main.temp) }}&deg;
      <p class="description">{{ description.description }}</p>

    </ion-card-content>
  </ion-card>

</template>

<script>
import { IonImg, IonCard, IonCardHeader, IonCardContent, IonCardSubtitle, IonCardTitle } from '@ionic/vue';

export default {
name: "CurrentWeather",
  components: {IonImg, IonCard, IonCardHeader, IonCardTitle,IonCardSubtitle,IonCardContent},
  props: ['description', 'main', 'town', 'sys']
}
</script>

<style scoped>



@media only screen and (max-width: 600px) {
  ion-card {
    width: 60vw;
    min-height: 80vw;
    margin: 0 auto;
  }

  ion-card-header {
    text-align: center;
    font-size: 6vw;
    font-family: "Courier New";
    font-weight: bold;
  }

  ion-img {
    width: 50%;
    margin: 0 auto;
  }

  .description {
    font-size: 4vw;
  }

  ion-card-content {
    text-align: center;
    font-size: 38px;
    padding-top: 0;
    font-family: inherit
  }

  ion-card-subtitle {
    text-align: center;
    margin: 0;
    font-size: 3vw;
    font-family: "Courier New"

  }
}

@media (min-width: 601px) {
  ion-card {
    width: 60vw;
    min-height: vw;
    margin: 0 auto;
  }
  ion-card-header {
    text-align: center;
    font-size: 4vw;
    font-family: "Courier New";
    font-weight: bold;
  }

  ion-img {
    width: 30%;
    margin: 0 auto;
  }

  .description {
    font-size: 2.5vw;
  }

  ion-card-content {
    text-align: center;
    font-size: 32px;
    padding-top: 0;
    font-family: inherit
  }

  ion-card-subtitle {
    text-align: center;
    margin: 0;
    font-size: 3vw;
    font-family: "Courier New"

  }
}

ion-card-title {

}


</style>
