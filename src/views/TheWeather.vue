<template>
  <ion-page>
    <ion-content :fullscreen="true">
      <form @submit.prevent="submitSearch()">
        <ion-toolbar>
          <ion-searchbar placeholder="Wpisz nazwę miasta" animated v-model="townInput"></ion-searchbar>
        </ion-toolbar>
      </form>
      <div v-if="error">
        <p>{{ error }}</p>
      </div>
      <div v-if="this.loading">
        <ion-spinner  name="crescent"></ion-spinner>
      </div>

      <transition name="weather" mode="out-in">
        <current-weather
            class="current"
            v-if="!this.loading && !this.isDetail"
            :description="weatherDescription"
            :main="weatherMain"
            :town="weatherTown"
            :sys="weatherSys">
          {{ day }}
        </current-weather>

        <current-weather-details
            class="current"
            v-else-if="!this.loading && this.isDetail"
            :description="weatherDescription"
            :main="weatherMain"
            :town="weatherTown"
            :wind="weatherWind"
            :sys="weatherSys">
        </current-weather-details>
      </transition>

      <ion-button v-if="!isDetail" @click="changeToDeTails()" shape="round" expand="block" >Pokaż detale</ion-button>
      <ion-button v-if="isDetail" @click="changeToDeTails()" shape="round" expand="block" >Wróć</ion-button>
    </ion-content>
  </ion-page>
</template>

<script>
import { Plugins } from '@capacitor/core'
const { Storage } = Plugins;
import { IonButton, IonPage, IonContent, IonSearchbar, IonToolbar, IonSpinner } from '@ionic/vue';
import axios from "axios";
import CurrentWeather from "@/components/CurrentWeather";
import CurrentWeatherDetails from "@/components/CurrentWeatherDetails";

export default {
  name: 'Tab1',
  components: {CurrentWeatherDetails, CurrentWeather, IonButton, IonContent, IonPage, IonSearchbar, IonToolbar, IonSpinner},
  beforeMount() {
    this.loading = true;
    Storage.get({key: 'townName'}).then((name) => { this.townName = name.value})
    .then(() => {
        this.getWeather();
    });
    this.day = this.today.toLocaleDateString();
  },
  data() {
    return {
      loading: false,
      isDetail: false,
      error: '',
      townName: '',
      townInput: '',
      weatherDescription: '',
      weatherTown: '',
      weatherWind: '',
      weatherMain: '',
      weatherSys: '',
      today: new Date(),
      day: ''
    }
  },
  methods: {
    submitSearch(){
      this.changeTown();
    },
    getWeather() {
      this.error = '';
      if (this.townName === null) {
        axios.get('http://api.openweathermap.org/data/2.5/weather?q=Warszawa&appid=7ded97f2e0ce975b4a0bc4630332feec&units=metric&lang=pl')
            .then((res) => {
              this.weatherDescription = res.data.weather[0];
              this.weatherMain = res.data.main;
              this.weatherTown = res.data.name;
              this.weatherSys = res.data.sys;
              this.weatherWind = res.data.wind;
            })
        .then(() => {
          this.loading = false;
        })
        .catch(() => {
          this.error = 'Złe miasto lub coś nie tak z połączeniem';
        })
      } else {
        axios.get('http://api.openweathermap.org/data/2.5/weather?q=' + this.townName +'&appid=7ded97f2e0ce975b4a0bc4630332feec&units=metric&lang=pl')
            .then((res) => {
              this.weatherDescription = res.data.weather[0];
              this.weatherMain = res.data.main;
              this.weatherTown = res.data.name;
              this.weatherSys = res.data.sys;
              this.weatherWind = res.data.wind;
            })
            .then(() => {
              this.loading = false;
            })
            .catch(() => {
              this.error = 'Złe miasto lub coś nie tak z połączeniem';
            })
      }
    },
    changeTown() {
      this.loading = true;
      Storage.set({ key: 'townName', value: this.townInput});
      Storage.get({key: 'townName'}).then((name) => { this.townName = name.value})
      .then(() => {
        this.getWeather();
      })
      .then(() => {
        this.townInput = '';
      })
    },
    changeToDeTails() {
      this.isDetail = !this.isDetail;
    }
  }
}

</script>

<style scoped>

ion-button {
  width: 50vw;
  margin: 5vw auto;
}

ion-toolbar {
  margin-top: 2vw;
}

@media only screen and (max-width: 600px) {
  .current {
    margin-top: 30%;
  }
}

@media (min-width: 601px) {
  .current {
    margin-top: 4vw;
  }
}

ion-img {
  width: 50vw;
}

ion-searchbar {
  width: 90%;
  margin: 0 auto;
}

.weather-enter-active {
  animation: changeDetails 1s ease-in;
}

.weather-leave-active {
  animation: changeDetails 1s ease-out reverse;
}

@keyframes changeDetails {
  0% {
    opacity: 0;
    transform: translateX(-300px) scale(0) skewY(180deg)
  }

  100% {
    opacity:1;
    transform: translateX(0px) scale(1)
  }
}
</style>

