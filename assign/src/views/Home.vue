<template>
  <div>
    <h2>ASSIGNMENT</h2>
    <b-container class="table">
      <b-row>
        <b-col>
          <div class="user">
              <input placeholder="User Name" type="text" v-model="newUser" style="height: 45px; width: 50%"><span>
              <b-button  @click="addUser">ADD</b-button></span>
          </div>
        </b-col>
        <b-col >
          <div class="list">
            <ul class="list-group listings">
              <b-list-group-item></b-list-group-item> 
             <li class="list-group-item" v-for="(user, index) in users" :key="index">
               {{user.name}}
            <span @click="delUser(user)" class="delUser">X</span></li>
        </ul>
          </div>
    </b-col>
   </b-row>
 </b-container>
</div>
</template>

<script>
// @ is an alias to /src
import axios from "axios"
export default {
  data(){
    return{
      users: [],
      newUser: '',
      userSelected: false

    };
  },
 async created(){
    // Get all users by making  a get request to/users
   let fetchUsers = await axios.get(
   "https://jsonplaceholder.typicode.com/users"
   );
   console.log(fetchUsers);
   this.users = fetchUsers.data;

  },
   methods: {
      addUser(){
      this.users.push({name: this.newUser});
      this.newUser = "";
      console.log(this.newUser)
      },
      delUser(user){
        this.userSelected = this.users.indexOf(user);
        this.users.splice(this.userSelected, 1)
      }
      
    },
 
  };
</script>
<style scoped>
.table{
  width: 50%;
 border: 1px solid black;
 background-color: blanchedalmond;
 border-radius: 20px;
}
.delUser{
  float: right;
  background-color: red;
   border-radius: 50%;
  font-weight: bolder;
  text-align: center;
  
}
.list-group.listings:hover{
cursor: pointer;
}
.user{
  margin-left: 2em;
  margin-top: 10px;
}
.list{
  margin-top: 10px;
}


</style>
