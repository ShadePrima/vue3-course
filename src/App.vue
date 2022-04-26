<template>
    <div class='app'>
        <post-form
        @create='createPost'
        />
        <post-list 
        :posts='posts'
        @remove='removePost'      
        />        
    </div>
</template>

<script>
import PostForm from '@/components/PostForm.vue'
import PostList from '@/components/PostList.vue'

    export default {
        components: {
            PostForm, PostList
            },
        data () {
            return {
                posts: [
                    {id: 1, title: 'JavaScript', body: 'Опсание поста' },
                    {id: 2, title: 'JavaScript 2', body: 'Опсание поста 2' },
                    {id: 3, title: 'JavaScript 3', body: 'Опсание поста 3' },
                    {id: 4, title: 'JavaScript 4', body: 'Опсание поста 4' },
                ],
            }
        },
        methods: {
            createPost(post) {
                this.posts.push(post)

            }, 
            removePost(post) {
                this.posts = this.posts.filter(p => p.id !== post.id)
            }
        }
    }
</script>

<style>

</style>
