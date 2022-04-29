<template>
    <div class='app'>
        <h1>Posting list</h1>
         <my-input
            v-model='searchQuery'
            placeholder='Search ... '
         />
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
        :posts='sortedAndSearchedPosts'
        @remove='removePost'
        v-if='!isPostsLoading'     
        />
 
        <div v-else>
            Loading ...
        </div>
        <div class='page__wrapper'>
            <div v-for='pageNumber in totalPages' 
                :key='pageNumber'
                class='page'
                :class='{
                    "current-page": page === pageNumber
                }'
                @click='changePage(pageNumber)'
                >
                {{ pageNumber }}
            </div> 
        </div>
    </div>
</template>

<script>
import PostForm from '@/components/PostForm.vue'
import PostList from '@/components/PostList.vue'
import MyDialog from './components/UI/MyDialog.vue'

import axios from 'axios'
import MySelect from './components/UI/MySelect.vue'
import MyInput from './components/UI/MyInput.vue'

    export default {
        components: {
            PostForm, PostList, MyDialog,
                MySelect,
                MyInput
            },
        data () {
            return {
                posts: [],
                dialogVisible: false,
                isPostsLoading: false,
                selectedSort: '',
                searchQuery: '',
                page: 1,
                limit: 10,
                totalPages: 0,
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
            changePage(pageNumber) { 
                this.page = pageNumber
            },
            async fetchPosts () {
                try {
                    this.isPostsLoading = true
                        const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                            params: {
                                _page: this.page,
                                _limit: this.limit
                            }
                        })
                        this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
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
        computed: {
            sortedPosts() {
                return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
            },

            sortedAndSearchedPosts () {
                return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
            }
        },           
        watch: {
           page() {
               this.fetchPosts()
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

.page__wrapper {
    display: flex;
    margin-top: 15px;
}

.page {
    border: 1px solid black;
    padding: 10px;
    border-radius: 5px;
}

.current-page {
    border: 2px solid teal;
}
</style>
