<template>
  <h2>Edit User</h2>
  <div class="div">
    <div class="mb-3">
      <label for="exampleInputEmail1" class="form-label">Name</label>
      <input
        type="text"
        class="form-control"
        v-model="newuser.name"
        id="exampleInputEmail1"
      />
    </div>
    <div class="mb-3">
      <label for="exampleInputEmail1" class="form-label">Email address</label>
      <input
        type="email"
        class="form-control"
        v-model="newuser.email"
        id="exampleInputEmail1"
      />
    </div>
    <div class="mb-3">
      <label for="exampleInputPassword1" class="form-label">Password</label>
      <input
        type="password"
        class="form-control"
        v-model="newuser.password"
        id="exampleInputPassword1"
      />
    </div>
    <div class="mb-3">
      <label for="exampleInputPassword1" class="form-label">Country</label>
      <select class="form-control" v-model="newuser.country" :value="newuser.country">
        <option>select</option>
        <option class="form-control">India</option>
        <option class="form-control">USA</option>
        <option class="form-control">UK</option>
      </select>
    </div>
    <div class="mb-3">
      Male <input type="radio" v-model="newuser.gender" value="Male" name="gender" />&nbsp; 
      Female <input type="radio" v-model="newuser.gender" value="Female" name="gender" />
    </div>
    <button type="submit" @click="UpdateUser()" class="btn btn-success">Update</button>
  </div>
</template>

<script>
//import firebase from '../Firebase';
import axios from 'axios';
export default {
  data() {
    return {
      newuser: {
        id:Math.random(),
        name: "",
        email: "",
        password: "",
        country: "",
        gender: "",
      },
    };
  },
  /*computed:{
    Edit(){
        return this.$store.getters.getEditData;
    }
  },*/
   mounted(){
    this.getpost();
    console.log(this.newuser)
    
  },
  methods: {
    async getpost(){
      const id = new URLSearchParams(window.location.search).get('id');
      await axios.get(`https://vue-form-6d470-default-rtdb.firebaseio.com/user/${id}.json`).then((response)=>{
       this.formateUserData(response.data);
      })
    },
    formateUserData(user){
      this.newuser = user;
      //console.log(this.users)
      
      },
    UpdateUser(){
      const id = new URLSearchParams(window.location.search).get('id');
        axios.put(`https://vue-form-6d470-default-rtdb.firebaseio.com/user/${id}.json`,this.newuser).then((response)=>{
            console.log(response);
            this.$router.push({path:'/user'})
        });
    }
    
  },
  
};
</script>

<style>
.div {
  margin-top: 45px;
  margin-left: 30%;
  margin-right: 30%;
  border: 1px solid;
  padding: 10px;
}
</style>