<template>
    <div class='app'>
        <h1>Posting list</h1>
        <my-button
        @click='showDialog'
        style='margin: 5px 0'
        >
        Create post
        </my-button>
        <my-dialog v-model:show='dialogVisible'>
            <post-form
            @create='createPost'
            />
        </my-dialog>
        
        <post-list
        :posts='posts'
        @remove='removePost'
        v-if='!isPostsLoading'     
        />
 
        <div v-else>
            Loading ...
        </div>   
    </div>
</template>

<script>
import PostForm from '@/components/PostForm.vue'
import PostList from '@/components/PostList.vue'
import MyDialog from './components/UI/MyDialog.vue'
import axios from 'axios'

    export default {
        components: {
            PostForm, PostList,
                MyDialog
            },
        data () {
            return {
                posts: [],
                dialogVisible: false,
                isPostsLoading: false,
            }
        }, 
        methods: {
            createPost(post) {
                this.posts.push(post)
                this.dialogVisible = false

            }, 
            removePost(post) {
                this.posts = this.posts.filter(p => p.id !== post.id)
            },
            showDialog() {
                this.dialogVisible = true
            },
            async fetchPosts () {
                try {
                    this.isPostsLoading = true
                        const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
                        this.posts = response.data
                        this.isPostsLoading = false
                } catch (e) {
                    alert('Error')
                }    
            }
        },
        mounted() {
            this.fetchPosts()
        }
    }
</script>

<style>

</style>
