<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Geo-Fence</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <div id="map" style="height: 100%; width: 100%"></div>
    </ion-content>
  </ion-page>
</template>

<script>
import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
} from "@ionic/vue";
export default {
  component: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
  },
  mounted() {
    this.initMap();
  },
  methods: {
    initMap() {
      const mapOptions = {
        center: { lat: -34.397, lng: 150.644 }, // Default center point
        zoom: 8, // Default zoom level
      };
      const map = new google.maps.Map(
        document.getElementById("map"),
        mapOptions
      );

      // Optionally, add markers, etc.
      new google.maps.Marker({
        position: { lat: -34.397, lng: 150.644 },
        map: map,
        title: "Hello World!",
      });
    },
  },
};
</script>

<style>
#map {
  height: 100%;
  width: 100%;
}
</style>
