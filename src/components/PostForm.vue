<template>
        <form @submit.prevent>
            <my-input 
            v-model="post.title"
            class="createPostInput"
            type="text"
            placeholder="Title"
            autofocus
            />
            <my-input 
            v-model="post.body"
            class="createPostInput"
            type="text" 
            placeholder="Description"
            />
            <my-button 
            @click="createPost"
            class="createPostButton" 
            >Create</my-button>
        </form>
</template>

<script>
export default {
    data() {
        return {
            post: {
            title: '',
            body: ''
            }
        }
    },
    methods: {
        createPost(event) {
            this.post.id = Date.now()
            this.$emit('create', this.post)
            this.post = {
                title: '',
                body: ''
            }
        },
    }
}
</script>

<style>
form {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
}
.createPostInput {
    margin-top: 15px;
}
.createPostButton {
    margin-top: 15px;
}
</style>