<template>
    <form @submit.prevent>
        <h4>Создание нового поста</h4>

        <input        
        v-model='post.title'     
        class='input'
        type='text'
        placeholder='Название'
        >

        <input 
        v-model='post.body'
        class='input'
        type='text'
        placeholder='Описание поста'
        >

        <my-button        
        style='align-self: flex-end; margin-top: 15px'
        @click='createPost'
        >
        Создать пост
        </my-button>
    </form>
</template>

<script>
import MyButton from './UI/MyButton.vue'
    export default {
        components: { MyButton },
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

.input {
    width: 100%;
    border: 1px solid teal;
    padding: 10px 15px;
    margin-top: 15px;
    border-radius: 5px;
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