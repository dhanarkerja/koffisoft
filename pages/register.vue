<template>
    <div>
        <div class="form-group">
            <label for="exampleInputEmail1">Email address</label>
            <input type="email" class="form-control" v-model="email" aria-describedby="emailHelp">
        </div>
        <div class="form-group">
            <label for="exampleInputEmail1">Mobile Phone Number</label>
            <input type="number" class="form-control" v-model="number" aria-describedby="emailHelp">
        </div>
            <div class="form-group">
            <label for="exampleInputEmail1">First Name</label>
            <input type="text" class="form-control" v-model="firstname" aria-describedby="emailHelp">
        </div>
        <div class="form-group">
            <label for="exampleInputEmail1">Last Name</label>
            <input type="text" class="form-control" v-model="lastname" aria-describedby="emailHelp">
        </div>
        <div class="form-group">
            <label for="exampleInputPassword1">Password</label>
            <input type="password" class="form-control" v-model="password" id="exampleInputPassword1">
        </div>
        <button type="submit" @click="submitUser()" class="btn btn-primary">Submit</button>
    </div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
      return {
          email:'',
          password:'',
          number:0,
          firstname:'',
          lastname:'',
      }
  },
  methods: {
     async submitUser() {
            // conifg for database type
           const config = {
                headers: {
                    'Content-Type': 'application/x-www-form-urlencoded'
                }
            };

            const res = await axios.post("http://202.157.184.201:8000/users",
                {
                    "email": this.email,
                    "hp": this.number,
                    "firstname": this.firstname,
                    "lastname": this.lastname,
                    "grup": "member",
                    "role": "string",
                    "tgl_lahir": "2022-04-07",
                    "jenis_kelamin": 1,
                    "password": this.password,
                    "referral_code": ""
                }
            )
            console.log(res.data.status.kode)
            if (res.data.status.kode == "success") {
                this.$router.push("/")
            }

      }
  }
}
</script>
