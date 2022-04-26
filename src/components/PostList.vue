<template>
    <div v-if='posts.length > 0'>
        <h3>Список пользователей</h3>
        <post-item 
        v-for='post in posts'
        :key='post.id'
        :post='post'
        @remove='$emit("remove", post)'
        />
    </div>
    <h2 v-else style='color: teal; text-align: center'>
        Список постов пуст
    </h2>
</template>

<script>
import PostItem from './PostItem.vue'
    export default {
        components: { PostItem },
        props: {
            posts: {
                type: Array,
                required: true,                
            }
        }        
    }
</script>

<style scoped>


</style>