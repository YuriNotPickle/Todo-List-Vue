<template>
  <div>
    <form @submit.prevent="create">
      <input class="text-input" type="text" placeholder="Title for a new note" v-model="noteTitle" />
      <button class="button button-green" type="submit">Create note</button>
    </form>
  </div>
</template>

<script>
  export default {
    name: "CreateTodo",
    data() {
      return {
        noteTitle: ""
      };
    },
    methods: {
      create() {
        this.$store.commit("CREATE_NEW_NOTE", this.noteTitle || "Untitled note");
        this.noteTitle = "";
      }
    }
  };
</script>

<style scoped>
   .text-input {
      border: 1px solid green;
      outline: 1px solid green ;
   }
</style>