<template>
    <ion-page>
        <ion-header>
            <ion-toolbar>
                <ion-title class="ion-text-center">Annulation</ion-title>
            </ion-toolbar>
        </ion-header>
        <ion-content :fullscreen="true">
            <ion-header collapse="condense">
                <ion-toolbar>
                    <ion-title size="large">Annulation</ion-title>
                </ion-toolbar>
            </ion-header>
            <IonGrid class="content ion-align-items-center">
                <IonCol>
                    <IonItem id="errors" color="danger" v-if="errorMsg">
                        <IonGrid>
                            <IonCol>
                                <IonText color="light" class="w-full">
                                    <h4 class="ion-text-center">{{ errorMsg }}</h4>
                                </IonText>
                            </IonCol>
                        </IonGrid>
                    </IonItem>
                    <IonItem id="success" color="success" v-if="successMsg">
                        <IonGrid>
                            <IonCol>
                                <IonText color="light" class="w-full">
                                    <h4 class="ion-text-center">{{ successMsg }}</h4>
                                </IonText>
                            </IonCol>
                        </IonGrid>
                    </IonItem>
                    <IonItem color="medium">
                        <IonLabel>Je confirme l'annulation</IonLabel>
                        <IonCheckbox v-model="confirm" color="primary"></IonCheckbox>
                    </IonItem>
                    <IonButton color="medium" expand="block" @click="sendData" >Annuler</IonButton>
                </IonCol>
            </IonGrid>
        </ion-content>
    </ion-page>
</template>

<script>

    import { IonPage, IonToolbar, IonTitle, IonHeader, IonContent, IonCheckbox, IonItem, IonLabel, IonButton, IonGrid, IonCol, IonText } from '@ionic/vue';
    export default {
        name: 'Cancel',
        components : { IonPage, IonToolbar, IonTitle, IonHeader, IonContent, IonCheckbox, IonItem, IonLabel, IonButton, IonGrid, IonCol, IonText },
        data() {
            return {
                confirm: false,
                errorMsg: null,
                successMsg: null
            }
        },
        methods: {
            sendData(){
                if(!this.confirm) return this.errorMsg = "Vous devez confirmer l'annulation.";
                fetch(`https://laravel-affluences-enzo.herokuapp.com/api/reservation/annulation/${this.$route.params.token}`, {
                        method: 'POST',
                        body: JSON.stringify({
                            confirm_cancel: "on"
                        }),
                            headers: {
                                'Accept': 'application/json',
                                'Content-Type': 'application/json'
                            },
                    })
                    .then(res => {
                        if(res.status == 204) return this.successMsg = "Annulation réussie.";
                        else return res.json();
                        })
                    .then(json => {
                        if(json.errors) this.errorMsg = json.errors.token[0];
                        })
                }
            }
    }
</script>

<style scoped>
    ion-button {
        margin-top:12px;
    }
    #errors, #success {
        border-radius:5px;
        margin-bottom: 6px;
    }
    ion-item {
        margin:0 2px;
    }
    .content {
        width:100%;
        height:100%;
        display:flex;
  }
</style>