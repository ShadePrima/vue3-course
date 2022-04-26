<template>
    <div class='app'>
        <h1>Страница с постами</h1>
        <my-button
        @click='showDialog'
        style='margin: 5px 0'
        >
        Создать пост
        </my-button>
        <my-dialog v-model:show='dialogVisible'>
            <post-form
            @create='createPost'
            />
        </my-dialog>
        
        <post-list
        :posts='posts'
        @remove='removePost'      
        />        
    </div>
</template>

<script>
import PostForm from '@/components/PostForm.vue'
import PostList from '@/components/PostList.vue'
import MyDialog from './components/UI/MyDialog.vue'

    export default {
        components: {
            PostForm, PostList,
                MyDialog
            },
        data () {
            return {
                posts: [
                    {id: 1, title: 'JavaScript', body: 'Опсание поста' },
                    {id: 2, title: 'JavaScript 2', body: 'Опсание поста 2' },
                    {id: 3, title: 'JavaScript 3', body: 'Опсание поста 3' },
                    {id: 4, title: 'JavaScript 4', body: 'Опсание поста 4' },
                ],
                dialogVisible: false,
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
            }
        }
    }
</script>

<style>

</style>
