<template>
    
<div class="app">
    <h1>Posts page</h1>
    <my-input 
    v-model="searchPostTitle"
    placeholder="Search..."
    class="findPost"
    />
    
    <my-dialog 
        v-model:show="dialogVisible"
    >
        <h1>New post</h1>
        <post-form
            @create="createPost"
        />
    </my-dialog>
    <div class="postListHead">
        <h2>Post list</h2>
        <div>
            <my-button
                @click="showDialog"
            >
                Create new post
            </my-button>
            <my-select
                v-model="selectSort"
                :options="sortOptions"
                class="selectSortPost"
            />
        </div>
    </div>
    <h1 class="createPostText">{{createPostText}}</h1>
    <post-list
    @remove="removePost"
    :posts="searchPost"
    />
</div>
</template>
<script>
import PostForm from "@/components/PostForm"
import PostList from "@/components/PostList"
export default {
    components: {
        PostForm, PostList
    },
    data() {
        return {
            posts: [
                // {id: 1, title: 'PostOne', body: 'DescriptionOne'},
                // {id: 2, title: 'PostTwo', body: 'DescriptionTwo'},
                // {id: 3, title: 'PostThree', body: 'DescriptionThree'},
                // {id: 4, title: 'PostThree', body: 'DescriptionThree'}
            ],
            dialogVisible: false,
            selectSort: '',
            sortOptions: [
                {value: 'title', name: 'Sort from title'},
                {value: 'body', name: 'Sort from description'}
            ],
            searchPostTitle: '',
            createPostText: 'Сlick on the button to create a post!'
        }
    },
    methods: {
        createPost(post) {
            if(this.posts.length == 0)
                this.createPostText = ''
            this.posts.push(post)
            this.dialogVisible = false
        },
        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id)
            if(this.posts.length == 0)
                this.createPostText = 'Сlick on the button to create a post!'
        },
        showDialog(event) {
            this.dialogVisible = true
        },
    },
    computed: {
        sortPost() {
            return [...this.posts].sort((p1, p2) => p1[this.selectSort]?.localeCompare(p2[this.selectSort]))
        },
        searchPost() {
            return this.sortPost.filter(p => p.title.toUpperCase().includes(this.searchPostTitle.toUpperCase()))
        }
    }
}
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Raleway:wght@400;700&family=Roboto&display=swap');
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Roboto', sans-serif;;
}
body {
    background-color: #d0d4d8;
    color: #2d2c30;
}
.app {
    padding: 30px;
}
h1 {
    display: inline;
}
.findPost {
    margin-top: 15px;
}
.postListHead {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-top: 15px;
}
.selectSortPost {
    margin-left: 15px;
}
.createPostText {
    display: block;
    margin-top: 15px;
}
</style>