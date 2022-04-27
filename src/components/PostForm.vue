<template>
    <form @submit.prevent>
        <h4>Create new post</h4>

        <my-input
        v-model='post.title' 
        type='text'
        placeholder='Name post'
        />

        <my-input
        v-model='post.body'
        type='text'
        placeholder='Post description'
        />

        <my-button        
        style='align-self: flex-end; margin-top: 15px'
        @click='createPost'
        >
        Create post
        </my-button>
    </form>
</template>

<script>

    export default {

        data () {
            return {
                post: {
                    id: '',
                    title: '',
                    body: ''
                }
            }
        },
        methods: {
            createPost () {
                this.post.id = Date.now()
                this.$emit('create', this.post)
                this.post = {
                    title: '',
                    body: ' '
                }
            }
        }
    }
</script>

<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}


.app {
    padding: 20px;
}

.hidden {
    display: none;
}

form {
    display: flex;
    flex-direction: column;
}


</style>