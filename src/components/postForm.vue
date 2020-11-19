<template>
    <div>

        <h3> create post </h3>
        <textarea v-model="content" cols="30" rows="10"></textarea>
        <br>
        <button @click="createpost()" :disabled= disable > create </button>

    </div>
</template>

<script>
import axios from "axios";
import cookies from "vue-cookies";
    export default {

        data() {
            return {
                content: "",
                disable:false,
            }
        },

        methods: {
            createpost() {
                this.disable=true;
                axios.request({
                    url:"https://innotechfullstack.ml/api/posts",
                    method:"POST",
                    data:{
                        "token":cookies.get("token"),
                        "content":this.content
                    }
                }).then(()=>{
                    location.reload();
                    this.disable=false

                }).catch((err)=>{
                    this.disable=false
                    console.log(err);})

                
            }
        },
        
    }
</script>

<style scoped>

</style>