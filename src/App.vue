<template>
    <div class='app'>
        <h1>Posting list</h1>
        <div class='app__btns'>
            <my-button
            @click='showDialog'
            >
            Create post
            </my-button>
            <my-select
                v-model='selectedSort'
                :options='sortOption'
            />
        </div> 
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
import MySelect from './components/UI/MySelect.vue'

    export default {
        components: {
            PostForm, PostList, MyDialog,
                MySelect
            },
        data () {
            return {
                posts: [],
                dialogVisible: false,
                isPostsLoading: false,
                selectedSort: '',
                sortOption: [
                    {value: 'title', name: 'By name'},
                    {value: 'body', name: 'By content'}
                ]
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
        },
        
           
        watch: {
            selectedSort(newValue) {
                this.posts.sort((post1, post2) => {
                    return post1[newValue]?.localeCompare(post2[newValue])
                }) 
            }
          
        }
    }
</script>

<style> 
* {
    margin: 0px;
    padding: 0px;
    box-sizing: border-box;
}

.app {
    padding: 20px;
}

.app__btns {
    margin: 15px 0;
    display: flex;
    justify-content: space-between;
}
</style>
