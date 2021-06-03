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
                    <ion-col>
                        <ion-button color="danger" @click="deleteBookmark">
                            <ion-icon slot="icon-only" :icon="trash"></ion-icon>
                        </ion-button>
                    </ion-col>
                </ion-row>
            </ion-grid>
        </ion-card-content>
    </ion-card>
</template>

<script lang="ts">
import firebase from 'firebase/app';
import 'firebase/firestore';

    import {
      IonIcon,
        IonCard,
        IonCardContent,
        IonButton,
        IonCol,
        IonRow,
        IonGrid
    } from '@ionic/vue'

    import { trash } from 'ionicons/icons'

    import { defineComponent } from 'vue';

    export default defineComponent ({
        name: "BookmarkedElement",
        components : {
          IonIcon,
            IonCard,
            IonCardContent,
            IonButton,
            IonCol,
            IonRow,
            IonGrid
        },
        setup() {
            return { trash }
        },
        methods:{
            deleteBookmark() {
             const db= firebase.firestore()
              //Suppression d'une ville dans la liste
              const querry = db.collection('cities').where('name', '==', "Lyon");
              querry.get().then(function(querySnapshot) {
                querySnapshot.forEach(function(doc) {
                  doc.ref.delete();
                });
              });
              console.log("test",querry);
            },},
        props:{
            city : String,
            tempMorning : String,
            tempAfternoon : String

        }
    })
</script>

<style scoped>

</style>