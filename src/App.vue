<template>
  <div id="app">

  </div>
</template>

<script>
import Hello from './components/Hello'
import Firebase from 'firebase'

let config ={
    apiKey: "AIzaSyByovdvO1h40MXJQVADprxqi0uMHNOm3EQ",
    authDomain: "inugayo-56a7f.firebaseapp.com",
    databaseURL: "https://inugayo-56a7f.firebaseio.com",
    projectId: "inugayo-56a7f",
    storageBucket: "inugayo-56a7f.appspot.com",
    messagingSenderId: "73025774043"
}

let app = Firebase.initializeApp(config);
let db = app.database();

let dogsRef= db.ref('dogs');

export default {
  name: 'app',
  firebase: {
    dogs: dogsRef
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
