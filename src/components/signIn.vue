<template>
    <div id="signin">
        <input type="text" v-model="username" placeholder="username">
        <input type="password" placeholder="password" v-model="password">
        <button @click="login_request()" type="submit" :disabled = disable> login</button>
        <p v-if="success"> you logged in successfully as {{ username }}</p>
        <p v-if="problem"> Something Went Wrong </p>

    </div>
</template>

<script>
import axios from "axios";
import cookies from "vue-cookies";
    export default {
        
        data() {
            return {
                username: "",
                password:"",
                disable:false,
                success: false,
                problem: false
            }},
            methods: {
                login_request() {
                    this.disable =true
                    axios.request({
                    url:"https://innotechfullstack.ml/api/login",
                    method: "POST",
                    data : {
                        "username": this.username,
                        "password": this.password
                    }
                }).then((res)=>{
                    this.success=true;
                    this.problem = false;
                    cookies.set("token",res.data.token);
                    cookies.set("userId",res.data.id);
                    location.reload();

                }).catch((err)=>{
                    this.problem = true;
                    this.disable=false;
                    console.log(err);
                    })
                    
                }
            },
        
    }
</script>

<style scoped>
 #signin{
        width: 70%;
    }
</style>