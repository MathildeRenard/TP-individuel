<template>
<Navbar></Navbar>

      <ion-input color="dark" placeholder="Entrez la ville à supprimer" @ionChange=onChange></ion-input>
  <ion-button color="danger"  @click="deleteBookmark">
    <ion-icon slot="icon-only" :icon="trash"></ion-icon>
  </ion-button>
</template>
<script lang="ts">
import Navbar from '@/views/Navbar';
import {trash} from 'ionicons/icons'
import firebase from 'firebase/app';
import 'firebase/firestore'
import {
  IonButton,
  IonIcon,
  IonInput,
} from '@ionic/vue'

import {
  starOutline,
  add
} from 'ionicons/icons'

import { defineComponent } from 'vue';

export default defineComponent({
  name: "supr",
  data() {
    return {
      city : ''
    }
  },
  components :{
    Navbar,
    IonButton,
    IonIcon,
    IonInput
  },
  props:{
    title : String
  },
  setup(){
    return {
      starOutline,
      add,
      trash
    }
  },
  methods : {
    onChange(e: any) {
      this.city = e.detail.value;
      console.log(this.city);
    },
    deleteBookmark() {
      const db = firebase.firestore()
      //Suppression d'une ville dans la liste
      const querry = db.collection('cities').where('name', '==', this.city);
      querry.get().then(function (querySnapshot) {
        querySnapshot.forEach(function (doc) {
          doc.ref.delete();
        });
      });

    },
  }
})

</script>

<style scoped>

</style>