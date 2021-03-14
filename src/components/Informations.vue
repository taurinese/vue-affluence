<template>
    <div id="terminal">
        <IonGrid>
            <IonRow>
                <div id="red-btn"></div>
                <div id="green-btn"></div>
            </IonRow>
        </IonGrid>
        <p v-if="infos"><span class="text-success">name:~$</span> <span color="light">{{ infos['name'] }}</span></p>
        <p v-if="infos"><span class="text-success">address:~$</span> <span color="light">{{ infos['address'] }}</span></p>
        <p v-if="infos"><span class="text-success">description:~$</span> <span color="light">{{ infos['description'] }}</span></p>
    </div>
</template>

<script>
import { IonGrid, IonRow } from '@ionic/vue'; 

    export default {
        components : { IonGrid, IonRow },
        props: [ 'infos' ]
    }
</script>

<style scoped>
    #terminal {
        margin:16px;
        background-color: #1F2A37;
        padding:12px;
        border-radius:5px;
    }
    #red-btn {
        background-color: #ED4444;
        width:15px;
        height:15px;
        border-radius:15px;
        content: "";
        margin-right: 10px;
    }
    #green-btn {
        background-color: #53B982;
        width:15px;
        height:15px;
        border-radius:15px;
        content: "";
    }
    .text-success {
        color:rgba(52, 211, 153);
        font-weight: bold;
    }
</style>