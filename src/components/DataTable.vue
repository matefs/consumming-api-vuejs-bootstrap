<template>
  <div class="container-fluid">
   <h1>List of users</h1>
   
<div class="table-responsive" :class="userDetails ? 'blur-class' : ''">
   <table class="table table-dark table-hover">
     <thead>
       <tr> 
         <th scope="col">Nome</th>
         <th scope="col">Email</th>
         <th scope="col">Cidade</th>
       </tr>
     </thead>
     <tbody>
       <tr v-for="user in usuarios" :key="user.id" @click="callUserDetails(user)">
   
         <td>{{ user.name }}</td>
         <td>{{ user.email }}</td>
         <td>{{ user.address.city }}</td>
       </tr>
     </tbody>
   </table>

</div>
   
   
<main v-if="userDetails" class='lightbox '>  
   
<div class="card card-details  ">
  <div class="row">
    <div class="col">

    <figure>
      <img src="https://cdn2.iconfinder.com/data/icons/4web-3/139/header-account-image-line-512.png" >
      <figcaption>{{SelectedUser.name}}</figcaption>
    </figure>

    </div>
    <div class="col second-column">
      <span>Username: {{SelectedUser.username}} </span>
      <span>E-mail: {{SelectedUser.email}} </span>
      <span>Website: {{SelectedUser.website}} </span>
      <span>Phone: {{SelectedUser.phone}} </span>
      <span>E-mail: {{SelectedUser.address.street}} </span>
      <span>Suite: {{SelectedUser.address.suite}} </span>
      <span>City: {{SelectedUser.address.city}} </span>
      <span>Zipcode: {{SelectedUser.address.zipcode}} </span>
      <span>Latitude: {{SelectedUser.address.geo.lat}} </span>
      <span>Longitude: {{SelectedUser.address.geo.lng}} </span>
    </div> 
  </div>
 
  
  <button class='btn btn-dark' @click="userDetails = !userDetails">Close User Details</button>
   
</div>
 

  </main>


 </div>
</template>

<script>
import axios from 'axios';

 export default {
  name: 'DataTable',
  data() {
    return {
      usuarios: String,
      userDetails: false,
      selectedUser: String,
    }
  },
  mounted() {
    axios.get("https://jsonplaceholder.typicode.com/users").then((res) => {
      this.usuarios = res.data;
      console.log(res.data);
    });
  },

  methods: {
    callUserDetails(user){
      this.userDetails = true;
      this.SelectedUser = user;
      // console.log(this.SelectedUser.name)
    }
  }
 }

</script>

<style>

.blur-class{
  z-index:0;
  filter:blur(10px);
}

.lightbox { 
  /* Overlay entire screen */
  position: fixed;  
  top: 0;
  left: 0;
  right: 0;
  bottom: 0; 
  /* Translucent background */
  background: rgba(0, 0, 0, 0.8);
}
  
 .card-details{
  font-size:1.3em; 
 }
 .card-details img {
  max-width:50%
 }

 .card-details span{ 
  display:block;
 }

 .second-column{ 
  text-align: left;
 }


</style>