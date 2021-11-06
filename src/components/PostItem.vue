<template>
    <div class="post">
        <div class="postText">
            <div><b>Title:</b> {{post.title}}</div>
            <div><b>Description:</b> {{post.body}}</div>
        </div>
        <my-button 
        @click="removePost" 
        >Remove</my-button>
    </div>
</template>

<script>
export default {
    props: {
        post: {
            type: Object,
            required: true
        }
    },
    methods: {
        removePost(event) {
            console.log(this.post)
            this.$emit('remove', this.post)
        }
    }
}
</script>

<style scoped>
    .post {
        display: flex;
        align-items: center;
        justify-content: space-between;
        max-height: 100%;
        color: #2d2c30;
        background-color: #e5eaee;
        border-radius: 10px;
        padding: 30px;
        margin-top: 15px;
    }
    .postText {
        max-height: 100%;
        margin-right: 30px;
    }
</style>