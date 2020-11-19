<template>
  <ion-card class="block_card">
    <div class="description">
      <slot name="description"></slot>
    </div>
    <div class="detail">
      <slot name="detail"></slot>
    </div>
  </ion-card>
</template>

<script>
import { IonCard, IonCardContent,  } from '@ionic/vue';

export default {
name: "WeatherDetailCard",
  components: {IonCard}
}
</script>

<style scoped>
.block_card {
  width: 90%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin: 1vw auto;
}

.description {
  margin-left: 1vw;
  opacity: 0.5;
}

.detail {
  margin-right: 7vw;
  align-self: center;
}
</style>
