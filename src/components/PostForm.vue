<template>
    <form @submit.prevent>
        <h4>Создание нового поста</h4>

        <my-input
        v-model='post.title' 
        type='text'
        placeholder='Название'
        />

        <my-input
        v-model='post.body'
        type='text'
        placeholder='Описание поста'
        />

        <my-button        
        style='align-self: flex-end; margin-top: 15px'
        @click='createPost'
        >
        Создать пост
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