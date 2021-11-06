<template>
<transition-group name="post-list">
    <post-item
    @remove="removePost"
    :post="post" 
    v-for="post in posts"
    :key="post.id"
    />
</transition-group>
</template>

<script>
import PostItem from "@/components/PostItem"
export default {
    components: {PostItem},
    props: {
        posts: {
            type: Array,
            required: true
        }
    },
    methods: {
         removePost(post) {
            console.log(post)
            this.$emit('remove', post)
        }
    }
}
</script>

<style scoped>
.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.5s ease;
}
.post-list-enter-from,
.post-list-leave-to {
    opacity: 0;
    position: absolute;
    transform: translateX(300px);
}
.post-list-move {
  transition: transform 0.5s ease;
}
</style>