<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Geofencing</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <ion-button @click="addGeofence">Add Geofence</ion-button>
    </ion-content>
  </ion-page>
</template>
<script>
import { Geofence } from "@ionic-native/geofence";
import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
} from "@ionic/vue";

export default {
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
  },
  name: "GeofencingPage",
  methods: {
    async addGeofence() {
      try {
        // Initialize geofence plugin
        await Geofence.initialize();

        // Define a geofence
        const geofence = {
          id: "unique_id",
          latitude: 37.285,
          longitude: -121.936,
          radius: 100,
          transitionType: 3, // 1: Enter, 2: Exit, 3: Both
          notification: {
            id: 1,
            title: "Geofence Event",
            text: "You have entered or exited a geofence",
            openAppOnClick: true,
          },
        };

        // Add the geofence
        await Geofence.addOrUpdate(geofence);
        console.log("Geofence added");
      } catch (error) {
        console.error("Error adding geofence", error);
      }
    },
  },
  mounted() {
    Geofence.onTransitionReceived().subscribe((geofences) => {
      geofences.forEach((geo) => {
        console.log("Geofence transition detected", geo);
      });
    });
  },
};
</script>

<style scoped>
ion-content {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
