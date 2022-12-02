<template>
  <div class="tablediv">
    <table class="table">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Name</th>
      <th scope="col">Email</th>
      <th scope="col">Password</th>
      <th scope="col">Country</th>
      <th scope="col">Gender</th>
      <th scope="col">Action</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(data, i) in users" :key="data.id">
      <th scope="row">{{i+1}}</th>
      <td>{{data.name}}</td>
      <td>{{data.email}}</td>
      <td>{{data.password}}</td>
      <td>{{data.country}}</td>
      <td>{{data.gender}}</td>
      <td> 
        <button class="btn btn-success" @click="edit(data.id)">Edit</button> &nbsp; 
        <button class="btn btn-danger" @click="Remove(data.id)">Delete</button>
      </td>
    </tr>
    
  </tbody>
</table>
  </div>
</template>

<script>
import axios from 'axios';
//import store from '../store/index';
export default {
  data(){
    return{
      users:''
    }
  },
  mounted(){
    this.getpost();
  },
  methods:{
    getpost(){
      axios.get(`https://vue-form-6d470-default-rtdb.firebaseio.com/user.json`).then((response)=>{
        this.formateUserData(response.data);
      })
    },
    formateUserData(user){
      this.users =[];
      console.log(user)
      for(let key in user){
        this.users.push({ ...user[key], id:key});
      }
      console.log(this.users)
    },
    Remove(id){
      axios.delete(`https://vue-form-6d470-default-rtdb.firebaseio.com/user/${id}.json`).then((response)=>{
        console.log(response)
      window.location.reload(true);
      })
    },
    edit(id){
      //const editaData = this.users.find((item)=>item.id ===id)
      //console.log(editaData)
      //store.dispatch('EditaData', editaData)
      this.$router.push({path:'/edit', query:{id:id}})
    },
  }

}
</script>

<style>
.tablediv{
  margin-left: 20%;
  margin-right:20%;
  border: 4px ;
}
</style>