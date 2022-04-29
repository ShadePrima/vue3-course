<template>
    <div class='post'>
        <!-- <div class='post__id'>{{post.id}}</div> -->
        <div>
            <div><strong>Name:</strong>{{post.title}}</div>        
            <div><strong>Description:</strong>{{post.body}}</div> 
        </div>
        <div class="post__btns">
            <my-button
            @click='$emit("remove", post)'
            >
            Delete
            </my-button>
        </div>         
    </div>
   
</template>

<script>

    export default {

        props: {
            post: {
                type: Object,
                required: true 
            }
        }
    }
</script>

<style scoped>
.post {
    padding: 15px;
    border: 2px solid teal;
    margin-top: 15px;
    border-radius: 5px;
    display: flex;
    align-items: center;    
    justify-content: space-between;
    min-width: 300px;
}
.post__btns {
    display: flex;  
}

.post__id {
    display: flex; 
    padding: 10px;
    margin: 10px;
    border: 1px solid teal;
    border-radius: 5px;
}
</style>