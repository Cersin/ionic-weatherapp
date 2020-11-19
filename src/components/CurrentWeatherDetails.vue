<template>
    <ion-card class="entire_card">
      <ion-card-content>
        <div class="weather_block">

          <WeatherDetailCard>
            <template v-slot:description>Temperatura</template>
            <template v-slot:detail>{{ Math.round(main.temp) }}&deg;</template>
          </WeatherDetailCard>

          <WeatherDetailCard :main="main">
            <template v-slot:description>Odczuwalna</template>
            <template v-slot:detail>{{ Math.round(main.feels_like) }}&deg;</template>
          </WeatherDetailCard>

          <WeatherDetailCard :main="main">
            <template v-slot:description>Minimalna</template>
            <template v-slot:detail>{{ Math.round(main.temp_min) }}&deg;</template>
          </WeatherDetailCard>

          <WeatherDetailCard :main="main">
            <template v-slot:description>Maksymalna</template>
            <template v-slot:detail>{{ Math.round(main.temp_max) }}&deg;</template>
          </WeatherDetailCard>

          <WeatherDetailCard :main="main">
            <template v-slot:description>Wilgotność</template>
            <template v-slot:detail>{{ main.humidity }}%</template>
          </WeatherDetailCard>

          <WeatherDetailCard :main="main">
            <template v-slot:description>Wiatr</template>
            <template v-slot:detail>{{ Math.round(wind.speed) }}km/h</template>
          </WeatherDetailCard>

          <WeatherDetailCard :main="main">
            <template v-slot:description>Wschód</template>
            <template v-slot:detail>{{ new Date(sys.sunrise * 1000).toLocaleTimeString().slice(0,5) }}</template>
          </WeatherDetailCard>

          <WeatherDetailCard :main="main">
            <template v-slot:description>Zachód</template>
            <template v-slot:detail>{{ new Date(sys.sunset * 1000).toLocaleTimeString().slice(0,5) }}</template>
          </WeatherDetailCard>


        </div>

      </ion-card-content>
    </ion-card>

</template>

<script>
import { IonCard, IonCardContent,  } from '@ionic/vue';
import WeatherDetailCard from "@/components/WeatherDetailCard";

export default {
  name: "CurrentWeatherDetails",
  components: {WeatherDetailCard, IonCard,IonCardContent},
  props: ['description', 'main', 'town', 'sys', 'wind']
}
</script>

<style scoped>

.weather_block {
  display: flex;
  flex-direction: column;


}

.entire_card {
  width: 60vw;
  min-height: 40vw;
  margin: 0 auto;
}

ion-card-title {

}

ion-card-content {

}

</style>
