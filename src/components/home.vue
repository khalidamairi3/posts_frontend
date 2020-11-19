<template>
    <div id="home">
        <postForm v-if=" token != undefined " />
        <pagePost v-for="post in posts" :key="post.id" :post = post /> 

    </div>
</template>

<script>
import postForm from "./postForm";
import pagePost from "./post"
import axios from "axios"
import cookies from "vue-cookies"
    export default {
        components: {
            pagePost,
            postForm
        },

        mounted () {
            axios.request({
                url:"https://innotechfullstack.ml/api/posts",
                method:"GET"

            }).then((response)=>{
                console.log(response);
                this.posts=response.data


            }).catch((err)=>{
                console.log(err);
            })



        },

        data() {
            return {
                posts:[]
            }
        },

        computed: {
            token() {
                return cookies.get("token"); 
            }
        },
     
        
    }
</script>

<style scoped>
#home{
    
}


</style>