<template>
<div class="app">
    <h1>Сраница с постами</h1>
    <my-input 
    placeholder="Поиск..."
    v-model="searchQuery"
    />
    <div class="post__btns">
         <my-button @click="showWindow" class="main__btn">Создать пост</my-button>
         <my-select 
            v-model="selectedSort"
            :options="sortOptions"
            >
        </my-select> 
    </div>
   
    <my-window v-model:show="windowVisible">
        <post-form 
@create="createPost" /> 
    </my-window>
     
<post-list 
v-bind:posts="sortedAndSearchedPosts"
@remove="removePost"
v-if="!isPostsLoading"
 />    
 <div v-else>Идет загрузка...</div>  
 </div>

</template>

<script>
import PostForm from "@/components/PostForm.vue"
import PostList from "@/components/PostList.vue"
import MyWindow from "./components/UI/MyWindow.vue";
import axios from 'axios'

export default {
  
    components: { PostForm, PostList, MyWindow },

    data() {
        return {
           posts: [],
           windowVisible: false,
           isPostsLoading: false,
           selectedSort: '',
           searchQuery: '',
           sortOptions: [
            {value: 'title', name: "По названию"},
            {value: 'body', name: "По содержимому"}
           ]
        }
    },
    methods: {
        createPost(post) {
            this.posts.push(post);
            this.windowVisible = false;    
    },
    removePost(post) {
        this.posts = this.posts.filter(p => p.id !== post.id)
    },
    showWindow() {
        this.windowVisible = true;
    },
    async fetchPosts() {
        try {
            this.isPostsLoading = true;
            setTimeout( async () => {
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
            this.posts = response.data;  
            this.isPostsLoading = false;    
            }, 500)
            
            
        }   catch (e) {
            alert('Ошибка')
        } finally {
            
        }
    }
    },
    mounted() {
        this.fetchPosts();
    },
    computed: {
        sortedPosts() {
            return [...this.posts].sort((post1,post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
        },
        sortedAndSearchedPosts() {
            return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
        }

    },
      
    
}

</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.app {
    padding: 20px;
}

.post__btns {
    display: flex;
    justify-content: space-between;
}



</style>