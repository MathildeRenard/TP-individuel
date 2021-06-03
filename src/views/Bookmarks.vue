<template>
    <ion-page>
        <Navbar :title="'bookmarks'">
        </Navbar>
      <ion-button color="danger" href="/supr">
        <ion-icon slot="icon-only" :icon="trash"></ion-icon>
      </ion-button>
        <ion-content v-if="cities.length>0">
            <BookmarkedElement v-for="(city,index) in cities" :key="index" :city="city.name" :tempMorning="'12,5°C'" :tempAfternoon="'21,5°C'">
            </BookmarkedElement>
        </ion-content>
    </ion-page>
</template>

<script>
import {options, trash} from 'ionicons/icons'
    import{
        IonPage,
        IonContent
    } from '@ionic/vue'

    import firebase from 'firebase/app'
    import 'firebase/firestore'
    import { DATABASE_CONFIGURATION } from '@/config.js';

    import Navbar from './Navbar';
    import BookmarkedElement from "@/views/BookmarkedElement";

    import { defineComponent } from 'vue';

    export const db = firebase.initializeApp(DATABASE_CONFIGURATION).firestore()

    export default defineComponent ({
        name: "Bookmarks",
        components : {
            IonPage,
            IonContent,
            Navbar,
            BookmarkedElement
        },
        data(){
            return {
                cities : []
            }
        },
        firestore: {
            cities : db.collection('cities'),
        },
      setup() {
        return { trash,options }
      },

    })

</script>

<style scoped>

</style>