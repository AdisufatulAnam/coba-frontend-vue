<template>
    <div class="container mt-custom">
        <div class="row">
            <div class="card border-0 rounded shodow">
                <div class="card-body">
                    <h4>DATA POST</h4>
                    <hr>
                    <router-link :to="{name: 'posts.create'}" class="btn btn-md btn-success">TAMBAH POSTS</router-link>
                    
                    <table class="table table-striped table-border mt-4">
                        <thead class="thead-dark">
                            <tr>
                                <th scope="col">TITLE</th>
                                <th scope="col">CONTENT</th>
                                <th scope="col">OPTIONS</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="(post, index) in posts" :key="index">
                                <th>{{ post.title }}</th>
                                <th>{{ post.content }}</th>
                                <td class="text-center"></td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import { onMounted, ref } from 'vue';
export default{
    setup(){
        //reactive stste
        let posts= ref([])
        
        //mouted
        onMounted(()=>{
            //penggil function getDataPosts
            getDataPosts()
        })
        //functiona "getDataPosts"
        function getDataPosts(){
            //get api from express back end 
            axios.get('http://localhost:3000/api/posts')
            .then(response => {
                
                //assign stste posts with response data
                posts.value = response.data.data
            }).catch(error => {
                console.log(error.response.data)
            })
        }
        //return
        return {
            posts, getDataPosts,
        }
    }

}
</script>
<style>
</style>