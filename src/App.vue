<template>
  <div id="app" class="container">
    <div class="page-header">
      <h1>Inugayo: A Canine Sanctuary</h1>
    </div>
    <div class="panel panel-default">
      <div class="panel panel-heading">
        Our dogs
      </div> 
      <div class="panel-body">
        <div class="table table-striped">
          <table>
            <thead>
             <tr>
               <th>Name</th>
               <th>Age</th>
               <th>Gender</th>
             </tr>
            </thead>
            <tbody>
              <tr v-for ="dog in dogs">
                <td>{{dog.name}}</td>
                <td>{{dog.age}}</td>
                <td>{{dog.gender}}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
    import Hello from './components/Hello'
    import Firebase from 'firebase'

    let config = {
        apiKey: "AIzaSyByovdvO1h40MXJQVADprxqi0uMHNOm3EQ",
        authDomain: "inugayo-56a7f.firebaseapp.com",
        databaseURL: "https://inugayo-56a7f.firebaseio.com",
        projectId: "inugayo-56a7f",
        storageBucket: "inugayo-56a7f.appspot.com",
        messagingSenderId: "73025774043"
    }

    let app = Firebase.initializeApp(config);
    let db = app.database();

    let dogsRef = db.ref('dogs');

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