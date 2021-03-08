<template>
    <div>
        <IonGrid v-if="horaires" class="ion-text-center">
            <IonRow>
                <IonCol>
                    Lundi
                </IonCol>
                <IonCol>
                    <span v-if="horaires.Lundi">
                        {{ horaires.Lundi.open }} - {{ horaires.Lundi.close }}
                    </span>
                    <span v-else>
                        Fermé
                    </span>
                </IonCol>
            </IonRow>
            <IonRow>
                <IonCol>
                    Mardi
                </IonCol>
                <IonCol>
                    <span v-if="horaires.Mardi">
                        {{ horaires.Mardi.open }} - {{ horaires.Mardi.close }}
                    </span>
                    <span v-else>
                        Fermé
                    </span>
                </IonCol>
            </IonRow>
            <IonRow>
                <IonCol>
                    Mercredi
                </IonCol>
                <IonCol>
                    <span v-if="horaires.Mercredi">
                        {{ horaires.Mercredi.open }} - {{ horaires.Mercredi.close }}
                    </span>
                    <span v-else>
                        Fermé
                    </span>
                </IonCol>
            </IonRow>
            <IonRow>
                <IonCol>
                    Jeudi
                </IonCol>
                <IonCol>
                    <span v-if="horaires.Jeudi">
                        {{ horaires.Jeudi.open }} - {{ horaires.Jeudi.close }}
                    </span>
                    <span v-else>
                        Fermé
                    </span>
                </IonCol>
            </IonRow>
            <IonRow>
                <IonCol>
                    Vendredi
                </IonCol>
                <IonCol>
                    <span v-if="horaires.Vendredi">
                        {{ horaires.Vendredi.open }} - {{ horaires.Vendredi.close }}
                    </span>
                    <span v-else>
                        Fermé
                    </span>
                </IonCol>
            </IonRow>
            <IonRow>
                <IonCol>
                    Samedi
                </IonCol>
                <IonCol>
                    <span v-if="horaires.Samedi">
                        {{ horaires.Samedi.open }} - {{ horaires.Samedi.close }}
                    </span>
                    <span v-else>
                        Fermé
                    </span>
                </IonCol>
            </IonRow>
            <IonRow>
                <IonCol>
                    Dimanche
                </IonCol>
                <IonCol>
                    <span v-if="horaires.Dimanche">
                        {{ horaires.Dimanche.open }} - {{ horaires.Dimanche.close }}
                    </span>
                    <span v-else>
                        Fermé
                    </span>
                </IonCol>
            </IonRow>
        </IonGrid>
    </div>
</template>

<script>
    import { IonGrid, IonCol, IonRow } from '@ionic/vue';

    export default {
        name: "Horaires",
        components: { IonGrid, IonCol, IonRow },
        props: [ 'horaires' ]
    }
</script>

<style scoped>
    ion-grid {
        background-color: #1F2A37;
        margin:16px;
        border-radius:5px;
    }
    ion-row {
        margin: 6px 0;
    }
    ion-col:first-child{
        font-weight:bold;
        color:rgba(52, 211, 153);
    }
</style>