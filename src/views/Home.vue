<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title class="ion-text-center">Accueil</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Accueil</ion-title>
        </ion-toolbar>
      </ion-header>
    
      <Informations v-model:infos="infos" />
      <Horaires v-model:horaires="horaires" />
      
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import Horaires from '@/components/Horaires';
import Informations from '@/components/Informations';

export default  {
  name: 'Home',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, Horaires, Informations },
  async created() {
    await fetch('https://laravel-affluences-enzo.herokuapp.com/api/infos')
    .then(res => res.json())
    .then(json => {
        this.horaires = json.horaires;
        this.infos = json;
        })
  },
  data() {
    return {
      horaires: null,
      name: null
    }
  },
}
</script>
