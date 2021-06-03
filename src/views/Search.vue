<template>
    <navbar :title="Add">
    </navbar>
    <!-- Default Searchbar -->
    <ion-searchbar @ionChange=onChange></ion-searchbar>
    <ion-button @click="addCity">Ajouter</ion-button>
</template>

<script lang="ts">
import firebase from 'firebase/app';
import 'firebase/firestore'
import {defineComponent} from "vue";
import {IonSearchbar, IonButton, toastController } from "@ionic/vue";
import Navbar from "@/views/Navbar.vue";
import weatherService from "@/services/weatherService";
const db = firebase.firestore();
    export default defineComponent ({
        name: "Search",
        data() {
          return {
              city : '',
              currentWeather : { cod : null }
          }
        },
        components:{
            Navbar,
            IonSearchbar,
            IonButton
        },
        methods : {
            onChange(e: any){
                this.city = e.detail.value;
            },
            async addCity(){
                this.currentWeather = await weatherService.getCityName(this.city);
                    const msg = await this.currentWeather.cod === '200' ? 'Votre saisie a bien été enregistrée' : 'erreur rencontrée';
                    this.PrintToast(msg);

              //ajout d'une nouvelle ville dans la liste
              await db.collection('cities').add({
                name: this.city})
            },
            async PrintToast(msg: string){
                const toast = await toastController
                    .create({
                        message: msg,
                        duration: 2000
                    })
                return toast.present();
            }
        }
    })

</script>

<style scoped>

</style>