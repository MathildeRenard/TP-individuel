<template>
    <ion-card>
        <ion-card-content>
            <ion-grid>
                <ion-row>
                    <ion-col>
                        <img src="../../public/assets/icon/sun.svg" alt="">
                        <p>{{ city }}</p>
                    </ion-col>
                    <ion-col>
                        <p>{{ tempMorning }}</p>
                        <p>{{ tempAfternoon }}</p>
                    </ion-col>
                </ion-row>
            </ion-grid>
        </ion-card-content>
    </ion-card>
</template>

<script lang="ts">


    import {
        IonCard,
        IonCardContent,
        IonCol,
        IonRow,
        IonGrid
    } from '@ionic/vue'
import {  options } from 'ionicons/icons'
    import { trash } from 'ionicons/icons'
    import { defineComponent } from 'vue';

    export default defineComponent ({
        name: "BookmarkedElement",
        components : {
            IonCard,
            IonCardContent,
            IonCol,
            IonRow,
            IonGrid
        },
        setup() {
            return { trash,options }
        },
        props:{
            city : String,
            tempMorning : String,
            tempAfternoon : String

        }
    })
</script>

<style scoped>

</style>