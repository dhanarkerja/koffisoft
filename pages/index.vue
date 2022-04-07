<template>
  <div>
    <div class="form-group">
        <label for="exampleInputEmail1">Email address</label>
        <input type="text" class="form-control" v-model="username" aria-describedby="emailHelp">
    </div>
    <div class="form-group">
        <label for="exampleInputPassword1">Password</label>
        <input type="password" class="form-control" v-model="password" id="exampleInputPassword1">
    </div>
    <button @click="login()" class="btn btn-primary">Submit</button>
    <button @click="register()" class="btn btn-primary">Register</button>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
      return {
          username:'',
          password:'',
          getResponse:[]
      }
  },
  methods: {
     async login() {
            // conifg for database type
            var qs = require('qs');
            var data = qs.stringify({
              'username': this.username,
              'password': this.password 
            });
            // using urlencoded
            var config = {
              method: 'post',
              url: 'http://202.157.184.201:8000/login',
              headers: { 
                'accept': 'application/json', 
                'Content-Type': 'application/x-www-form-urlencoded'
              },
              data : data
            };

            const res = await axios(config)
            console.log(res.data.status.kode)
            if(res.data.status.kode == "success") {
              this.$router.push("/dashboard")
            }
      },
      register(){
        this.$router.push("/register")
      }
  }
}
</script>
