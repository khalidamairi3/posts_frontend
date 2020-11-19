<template>
    <div id="signup">

        <input type="text" v-model="username" placeholder="username">
        <input type="password" placeholder="password" v-model="password">
        <button @click="signup_request()" type="submit" :disabled = disable> sign up</button>
        <p v-if="success"> user has been registered succeesfully</p>


    </div>
</template>

<script>
import axios from "axios"
    export default {
        data() {
            return {
                username: "",
                password:"",
                disable:false,
                success: false
            }
        },
        methods: {
            signup_request() {
                this.disable=true;
                axios.request({
                    url:"https://innotechfullstack.ml/api/users",
                    method: "POST",
                    data : {
                        "username": this.username,
                        "password": this.password
                    }
                }).then(()=>{
                    this.success=true;

                }).catch((err)=>{
                    console.log(err);
                })

                
                
            }
        },
        
    }
</script>

<style scoped>
    #signup{
        width: 70%;
    }
</style>