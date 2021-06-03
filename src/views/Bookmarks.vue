<template>
    <ion-page>
        <Navbar :title="'bookmarks'">
        </Navbar>
        <ion-content v-if="cities.length>0">
            <BookmarkedElement v-for="(city,index) in cities" :key="index" :city="city.name" :tempMorning="'12,5°C'" :tempAfternoon="'21,5°C'">
            </BookmarkedElement>
        </ion-content>
    </ion-page>
</template>

<script>
    import{
        IonPage,
        IonContent
    } from '@ionic/vue'

    import firebase from 'firebase/app'
    import 'firebase/firestore'
    import { DATABASE_CONFIGURATION } from '@/config.js';
    export const db = firebase.initializeApp(DATABASE_CONFIGURATION).firestore()

    import Navbar from './Navbar';
    import BookmarkedElement from "@/views/BookmarkedElement";

    import { defineComponent } from 'vue';



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


    })

</script>

<style scoped>

</style>