<template>
    <div id="post" >
        <h4> {{post.username }} </h4>
        <p>{{post.content}}</p>
        <button @click="update = true " v-if="post.user_id == userId"> Edit </button>
        <button @click="deletePost(post.id)" v-if="post.user_id == userId" :disabled = delete_disable> Delete </button>
        <div v-if="update"> 
            <textarea v-model="content" cols="30" rows="10"></textarea>
            <button @click="updatePost(post.id)" :disabled= update_disable> update </button>

        </div>
    </div>
</template>

<script>
import cookies from "vue-cookies";
import axios from "axios"
    export default {
        props: {
            post: {
                type: Object,
                required:true 
            },
        },
        data() {
            return {
                userId: cookies.get("userId"),
                update : false,
                content:"",
                update_disable:false,
                delete_disable:false
            }
        },
        methods: {
                updatePost(id) {
                    this.update_disable=true
                    axios.request({
                        url:"https://innotechfullstack.ml/api/posts",
                        method:"PATCH",
                        data:{
                            "postId":id,
                            "content":this.content,
                            "token": cookies.get("token")


                        }
                    }).then((res)=>{
                        this.update = false
                        this.post.content = res.data.content;
                        this.update_disable =false
                    }).catch((err)=>{
                        console.log(err);
                        this.update_disable= false;
                    
                    })

                
            },
            deletePost(id){
                this.delete_disable=true
                    axios.request({
                        url:"https://innotechfullstack.ml/api/posts",
                        method:"DELETE",
                        data:{
                            "postId":id,
                            "token": cookies.get("token")


                        }
                    }).then(()=>{
                        this.delete_disable =false
                        location.reload();
                    }).catch((err)=>{
                        console.log(err);
                        this.delete_disable= false;
                    
                    })


            }
        },
    }
</script>

<style scoped>
#post{
    width: 50%;
    border-bottom: 2px solid gray ;
    margin-left: 25%;
}

</style>