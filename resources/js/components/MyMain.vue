<template>
    <div class="container">
        <div v-if="this.loading" class="d-flex justify-content-center">
            <div class="spinner-border text-primary" role="status">
                <span class="sr-only">Loading...</span>
            </div>
        </div>
        <div v-else class="card p-3" v-for="(post, index) in posts" :key="index">
            <h2>{{post.title}}</h2>
            <p>{{truncateText(post.content, 100)}}</p>
            <h4>{{(post.category)?post.category.name:'Nessuna categoria'}}</h4>
            <ul>
                <li v-for="(tag, index) in post.tags" :key="index">{{tag.name}}</li>
            </ul>
        </div>
    </div>
</template>

<script>
    export default {
        name:'MyMain',
        data(){
            return{
                posts:[],
                loading: true,
            }
        },
        methods:{
            getPosts(){
                axios.get('/api/posts')
                .then((response)=>{
                    this.posts = response.data.results;
                    this.loading = false;
                });
            },

            truncateText(text, maxlength){
                if(text.length > maxlength){
                    return text.substring(0, maxlength) + '...';
                }else{
                    return text;
                }
            }
        },
        mounted(){
            this.getPosts();
        },
    }
</script>

<style>

</style>
