<template>
    <div class="container">
        <h1>Comentários</h1>
        <hr />
        <FormTodo v-on:add-todo="addComment" />
        <div class="list-group">
            <p v-if="Comments.length <= 0">Sem comentários...</p>
            <div class="list-group-item" v-for="(comment, index) in allComments" v-bind:key="index">
                <span class="comment__author">Autor: <strong>{{ comment.name }}</strong></span>
                <p>{{ comment.message }}</p>
                <div>
                <a href="#" v-on:click.prevent="removeComment(index)" title="Excluir">Excluir</a>
                </div>
            </div>
        </div>
        <hr />
    </div>
</template>

<script>
import FormTodo from "./FormTodo"
export default{
    components: {
        FormTodo
    },
    data() {
            return {
                Comments: [],
            }
        },
    methods: {
        addComment(comment){
            this.Comments.push(comment);
        },
        removeComment(index) {
            this.Comments.splice(index, 1);
        }
    },
    computed: {
        allComments(){
            return this.Comments.map(comment => ({
                ...comment,
                name: comment.name.trim() === '' ? 'Anônimo' : comment.name
            }))
        }
    },
    watch: {
        Comments(val){
            console.log('val', val);
            
        }
    }
}
</script>