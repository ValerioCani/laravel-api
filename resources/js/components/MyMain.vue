<template>
    <div class="container">
        <div class="card p-3" v-for="(post, index) in posts" :key="index">
            <h2>{{post.title}}</h2>
            <p>{{post.content}}</p>
            <h4>{{(post.category)?post.category.name:'-'}}</h4>
        </div>
    </div>
</template>

<script>
    export default {
        name:'MyMain',
        data(){
            return{
                posts:[]
            }
        },
        methods:{
            getPosts(){
                axios.get('/api/posts')
                .then((response)=>{
                    this.posts = response.data.results;
                });
            }
        },
        mounted(){
            this.getPosts();
        },
    }
</script>

<style>

</style>
