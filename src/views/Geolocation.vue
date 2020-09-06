<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <IonButtons>
          <ion-back-button />
        </IonButtons>
        <ion-title>Geolocation</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true" class="ion-padding">
      <h2>This is the Geolocation Page</h2>
      <div>Showing the use of the Capacitor Geolocation plugin and the vue-router for changing pages in the application</div>
      <pre v-if="location">{{location.coords.latitude}} : {{location.coords.longitude}}</pre>
      <ion-button @click="getLocation">Get Current Location</ion-button>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
  IonButtons,
  IonButton,
  IonBackButton,
} from "@ionic/vue";
import { defineComponent, ref } from "vue";
import { Plugins } from "@capacitor/core";
const { Geolocation } = Plugins;

export default defineComponent({
  name: "Geolocation",
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonButtons,
    IonBackButton,
    IonButton,
  },
  setup() {
    const location = ref<any | null>(null);
    const getLocation = async () => {
      console.log("got getLocation event");
      location.value = await Geolocation.getCurrentPosition({
        enableHighAccuracy: true,
        timeout: 30000,
      });
      console.log("location", location.value.coords);
    };

    return {
      location,
      getLocation,
    };
  },
});
</script>

<style scoped>
</style>