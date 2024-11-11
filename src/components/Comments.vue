<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="container">
    <h1>Comentários</h1>
    <hr />
    <FormTodo v-on:add-todo="addComment"></FormTodo>
    <div class="list-group">
      <p v-if="comments.length <= 0">Ainda Sem Comentários...</p>
      <div
        class="list-group-item"
        v-for="(comment, index) in allComments"
        v-bind:key="index"
      >
        <span class="comment__author"
          >Autor: <strong>{{ comment.name }}</strong></span
        >
        <p>{{ comment.message }}</p>
        <div>
          <a href="#" title="Excluir" v-on:click.prevent="removeComment(index)"
            >Excluir</a
          >
        </div>
      </div>
    </div>
    <hr />
  </div>
</template>

<script>
import FormTodo from "./FormTodo.vue";
export default {
  components: { FormTodo },
  data() {
    return {
      comments: [],
    };
  },
  methods: {
    addComment(comment) {
      this.comments.push(comment);
    },
    removeComment(index) {
      this.comments.splice(index, 1); //método que vai remover 1 item da posição index
    },
  },
  computed: {
    //essa propriedade é basicamente para customizar o que vai ser mostrado na view
    allComments() {
      return this.comments.map((comment) => ({
        ...comment,
        name: comment.name.trim() === "" ? "Anônimo" : comment.name,
      }));
    },
  },
  // watch: {
  //   comments(newVal) {
  //     console.log("Comentários atualizados:", newVal);
  //   },
  // },
};
</script>
