<template>
    <div>
        <IonItem id="errors" color="danger" v-if="errorMsg.length > 0">
            <IonGrid>
                <IonCol>
                    <IonText v-for="error in errorMsg" :key="error" color="light" class="w-full">
                        <h4 class="ion-text-center">{{ error }}</h4>
                    </IonText>
                </IonCol>
            </IonGrid>
        </IonItem>
        <IonItem id="success" color="success" v-if="successMsg">
            <IonGrid>
                <IonCol>
                    <IonText color="light" class="w-full">
                        <h4 class="ion-text-center">{{ successMsg }}</h4>
                        <a class="ion-text-center" :href="'/annulation/' + token">Vous voulez annuler?</a>
                    </IonText>
                </IonCol>
            </IonGrid>
        </IonItem>
        <IonItem color="medium">
            <IonLabel>Date de réservation</IonLabel>
            <IonDatetime 
                displayFormat="YYYY-MMM-DDTHH:mm" 
                minuteValues="00" 
                monthShortNames="jan, fev, mars, avril, mai, juin, juillet, aout, sept, oct, nov, dec"
                cancelText="annuler"
                doneText="valider"
                v-model="selectedDate"
                :min="currentDate"
            ></IonDatetime>
        </IonItem>
        <IonItem color="medium">
          <IonLabel position="floating">Adresse mail</IonLabel>
          <IonInput v-model="email" name="email" type="email"></IonInput>
        </IonItem>
        <IonItem color="medium">
            <IonLabel>J'ai lu et accepté les CGU</IonLabel>
            <IonCheckbox v-model="cgu" color="primary"></IonCheckbox>
        </IonItem>

        <IonButton color="medium" expand="block" @click="sendData" >Réserver</IonButton>
    </div>
</template>

<script>
    import { IonItem, IonLabel, IonInput, IonButton, IonDatetime, IonCheckbox, IonText, IonGrid, IonCol } from '@ionic/vue';

    export default {
        name: "BookingForm",
        components: { IonItem, IonLabel, IonInput, IonButton, IonDatetime, IonCheckbox, IonText, IonGrid, IonCol },
        data() {
            return {
                selectedDate: '',
                email: '',
                cgu: false,
                errorMsg: [],
                successMsg: null,
                token: null,
                currentDate: new Date(Date.now()).toISOString()
            }
        },
        methods: {
            validateEmail(email) {
                const re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
                return re.test(String(email).toLowerCase());
            },
            sendData(){
                this.errorMsg = [];
                this.successMsg = null;
                if(!this.validateEmail(this.email)) this.errorMsg.push("Veuillez entrer un email valide.");
                if(!this.cgu) this.errorMsg.push("Veuillez accepter les CGU.");
                if(this.errorMsg.length > 0) return;
                let data = {
                    datetime: this.selectedDate.substring(0, 16),
                    cgu: "on",
                    email: this.email
                };
                fetch('https://laravel-affluences-enzo.herokuapp.com/api/reservation', {
                    method: 'POST',
                    body: JSON.stringify(data),
                        headers: {
                            'Accept': 'application/json',
                            'Content-Type': 'application/json'
                        },
                })
                .then(res => res.json())
                .then(json => {
                    if(json.status) this.successMsg = json.message;
                    else this.errorMsg = json.messages;
                    this.token = json.token;
                    })
            }
        },
    }
</script>

<style scoped>
    .w-full {
        width:100%;
    }
    #errors, #success {
        border-radius:5px;
        margin-bottom: 6px;
    }
    ion-item {
        margin:0 2px;
    }
    ion-button {
        margin-top:12px;
    }
</style>