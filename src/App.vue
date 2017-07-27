<template>
  <div id="app" class="container">
    <div class="page-header">
      <h1><strong>Inugayo:</strong> A Canine Sanctuary</h1>
    </div>

    <!-- Add Dogs Panel -->
    <div class="panel panel-default">
      <div class="panel panel-heading"><h3>Add Dog</h3> </div>
      <div class="panel panel-body">
        <form id="form" class="form-inline" v-on:submit.prevent="addDog">
          <div class="form-group">
            <label for="dogName">Name: </label>
            <input type="text" id="dogName" class="form-control" v-model="newDog.name">
          </div>
          <div class="form-group">
            <label for="dogBreed">Breed: </label>
            <input type="text" id="dogBreed" class="form-control" v-model="newDog.breed">
          </div>
          <div class="form-group">
            <label for="dogAge">Age: </label>
            <input type="text" id="dogAge" class="form-control" v-model="newDog.age">
          </div>
          <div class="form-group">
            <label for="dogGen">Gender: </label>
            <input type="text" id="dogGen" class="form-control" v-model="newDog.gender">
          </div>
          <input type="submit"class="btn btn-primary" value="Add Dog">
        </form>
      </div>
    </div>

    <!-- Available Dogs Panel -->
    <div class="panel panel-default">
      <div class="panel panel-heading">
        <h3>Available Dogs</h3>
      </div> 
      <div class="panel-body">
        <table class="table table-striped">
            <thead>
             <tr>
               <th>Name</th>
               <th>Age</th>
               <th>Gender</th>
               <th>Breed</th>
               <th>Remove</th>
             </tr>
            </thead>
            <tbody>
              <tr v-for ="dog in dogs">
                <td>{{dog.name}}</td>
                <td>{{dog.age}}</td>
                <td>{{dog.gender}}</td>
                <td>{{dog.breed}}</td>
                <td><span class="glyphicon glyphicon-trash" v-on:click="removeDog(dog)"></span></td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
</template> // SCRIPTS
<script>
    import Hello from './components/Hello'
    // import Firebase
    import Firebase from 'firebase'

    //import Toastr
    import toastr from 'toastr'

    //config Firebase
    let config = {
            apiKey: "AIzaSyByovdvO1h40MXJQVADprxqi0uMHNOm3EQ",
            authDomain: "inugayo-56a7f.firebaseapp.com",
            databaseURL: "https://inugayo-56a7f.firebaseio.com",
            projectId: "inugayo-56a7f",
            storageBucket: "inugayo-56a7f.appspot.com",
            messagingSenderId: "73025774043"
        }
        //initialize Firebase
    let app = Firebase.initializeApp(config);
    //set Firebase as database for app
    let db = app.database();
    //reference dogs in database
    let dogsRef = db.ref('dogs');

    export default {
        name: 'app',
        firebase: {
            //set nickname for dog reference
            dogs: dogsRef
        },
        data() {
            return {
                newDog: {
                    name: "",
                    gender: "",
                    age: '',
                    breed: ""
                }
            }
        },
        methods: {
            //Add Dogs function
            addDog: function() {
                dogsRef.push(this.newDog);
                this.newDog.name = "";
                this.newDog.age = "";
                this.newDog.breed = "";
                this.newDog.gender = "";
                toastr.success("Dog Added!");
            },
            //Remove Dog function
            removeDog: function(dog) {
                dogsRef.child(dog['.key']).remove();
                toastr.error("Dog Removed!");
            }
        }
    }
</script>

// STYLES
<style>
    #app {
        font-family: 'Montserrat', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: #2c3e50;
        margin-top: 60px;
    }
    
    .glyphicon.glyphicon-trash {
        color: darkred;
    }
</style>