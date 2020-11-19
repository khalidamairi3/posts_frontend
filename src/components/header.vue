<template>
  <div>
    <div id="header">
      <h2>FULL STACK BLOG POST</h2>
      <button v-if="userId == undefined " @click="login=true; signup = false">Log in</button>
      <button v-if="userId == undefined " @click="login=false; signup = true">sign up</button>
      <button v-if="userId != undefined " @click="logout()"> logout </button>
    </div>
    <signup v-if="signup  && userId == undefined" />
    <signIn v-if="login && userId == undefined" />
  </div>

</template>

<script>
import signIn from './signIn'
import signup from './signup.vue';
import cookies from 'vue-cookies';
import axios from "axios";
export default {
  components: { signup,
  signIn },

    data() {
        return {
            login: false,
            signup: false,
        }
    },
    computed: {
        userId() {
            return cookies.get("userId"); 
        }
    },
    methods: {
        logout() {
            axios.request({
                url:"https://innotechfullstack.ml/api/login",
                method:"DELETE",
                data:{
                    "token":cookies.get("token")
                }
            }).then(()=>{
                this.login = false;
                this.signup =false;
                cookies.remove("userId");
                cookies.remove("token")
            }).catch((err)=>{console.log(err);})
            
        }
    },
};
</script>

<style scoped>
#header {
    margin-top:0 ;
    padding-top: 0;
    height: 10vh;
  display: grid;
  grid-template-columns: 4fr 1fr 1fr;
}
button{
    margin-top:2.5vh;
    width: 50%;
    height: 50%;

}
</style>