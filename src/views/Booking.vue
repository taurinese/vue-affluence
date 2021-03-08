<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title class="ion-text-center">Réservation</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Réservation</ion-title>
        </ion-toolbar>
      </ion-header>
      <IonGrid class="ion-align-items-center">
        <IonCol>
          <BookingForm />
        </IonCol>
      </IonGrid>
      
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonGrid, IonCol} from '@ionic/vue';
import BookingForm from '@/components/BookingForm';

export default {
  name: 'Booking',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, BookingForm, IonGrid, IonCol }
}
</script>
<style scoped>
  ion-grid {
    width:100%;
    height:100%;
    display:flex;
  }
</style>
