<template>
<div id="container">
<h1>Usuarios</h1>
<input type="text" class="form-control" v-model="id">
<input type="text" class="form-control" v-model="name">
<input type="text" class="form-control" v-model="username">
<input type="text" class="form-control" v-model="email">
<button class="btn-primary" @click="add">AGREGAR</button>
<br>
<hr>
<table class="table">
  <thead>
    <tr > 
      <th scope="col">ID</th>
      <th scope="col">NAME</th>
      <th scope="col">USER NAME</th>
      <th scope="col">EMAIL</th>
    </tr>
  </thead>
  <tbody >
    <tr v-for="user in data" :key="user">
      <th scope="row">{{user.id}}</th>
      <td>{{user.name}}</td>
      <td>{{user.username}}</td>
      <td>{{user.email}}</td>
    </tr>
    
  </tbody >
</table>

</div>
</template>

<script>
import {ref} from 'vue';
import axios from "axios";
export default {
name:"Users",
setup(){
let data = ref([]);
let id=ref("");
let name=ref("");
let username=ref("");
let email=ref("");

const list=()=>{
  axios.get("https://jsonplaceholder.typicode.com/users").then(response=>{
      data.value=response.data;
  })
};

const add =()=>{
    if (
    id.value==""||
    name.value==""||
    username.value==""||
    email.value==""
    ) {
      window.Swal.fire({
    icon: 'error',
    title: 'Oops...',
    text: 'Something went wrong!',
    footer: '<a href="">Why do I have this issue?</a>'
      }
      )  ;
        
    } else {
     data.value.push({
     id:id.value,
     name:name.value,
     username:username.value,
     email:email.value
 });
  id.value="",
 name.value="",
 username.value="",
 email.value=""
 
 window.Swal.fire({
  position: 'top-end',
  icon: 'success',
  title: 'Your work has been saved',
  showConfirmButton: false,
  timer: 1500
})
    }
}

list();
return{data,add,id,name,username,email}
},
}
</script>

<style>
</style>