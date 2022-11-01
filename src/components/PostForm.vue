<template>
    <div>
        <form @submit.prevent>
            <h4>Создание поста</h4>
            <my-input 
            v-model="post.title" 
            type="text" 
            placeholder="Название"/>
            <my-input  
            v-model="post.body"
            type="text" 
            placeholder="Описание"/>
            <my-button class="btn" @click="createPost">Создать</my-button>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            post: {
                title: "",
                body: "",
            }
        };
    },
    methods: {
        createPost() {
            this.post.id = Date.now();
            this.$emit("create", this.post);
            this.post = {
                title: "",
                body: "",
            };
        }
    },

}
</script>

<style>
form {
    
    display: flex;
    flex-direction: column;
}



.btn {
    background: none;
    align-self: flex-end;
    width: 150px;
    height: 50px;
    color: teal;
}


</style>