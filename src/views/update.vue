<template>
  <Navbar></Navbar>

  <ion-input color="dark" placeholder="Entrez le nom de la ville à modifier" @ionChange=onChange></ion-input>
  <ion-input color="dark" placeholder="Entrez le nom de la ville modifié" @ionChange=modifier></ion-input>
  <ion-button color="dark" @click=updateCity>
    modifier
  </ion-button>
  <p>{{msg}}</p>
</template>
<script>
import Navbar from '@/views/Navbar.vue';
import firebase from 'firebase/app';
import 'firebase/firestore'
import {
  IonButton,
  IonInput,
} from '@ionic/vue'

import {
  starOutline,
  add
} from 'ionicons/icons'

import { defineComponent } from 'vue';

export default defineComponent({
  name: "update",
  data() {
    return {
      city : '',
      msg : '',
      new : ''
    }
  },
  components :{
    Navbar,
    IonButton,
    IonInput
  },
  props:{
    title : String
  },
  setup(){
    return {
      starOutline,
      add,
    }
  },
  methods : {
    onChange(e) {
      this.city = e.detail.value;
      console.log(this.city);
    },
    modifier(e) {
      this.new = e.detail.value;
      console.log(this.new);
    },

    updateCity() {
      const old = this.city
      const up = this.new
      const db = firebase.firestore()
      //mise à jour d'une ville dans la liste
      const querry = db.collection('cities').where('name', '==', old);
      querry.get().then(function (querySnapshot) {
        querySnapshot.forEach(function (doc) {
          doc.ref.update({name: up})
        });
      });
      this.msg = "La ville a bien été modifiée";
    }
  }
});

</script>

<style scoped>

</style>