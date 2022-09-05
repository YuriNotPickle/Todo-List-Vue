<template>
  <div class="note-view">
    <div class="note-header">
      <div class="note-title">
         <p>{{note.title || 'Untitled note'}}</p>
         <router-link
          :to="{name: 'Edit', params: {id: note.id}}"
          class="button button-green"
        >Edit</router-link>
         <button @click="deleteNote" class="button button-red">Delete</button>
        <DeleteNoteModal
          :isDeleteModalVisible="isDeleteModalVisible"
          :note="this.note"
          v-on:deleteModalClosed="closeModal"
        />
      </div>
    </div>
    <div class="note-view-todo-list">
      <TodoView v-for="todo in firstThreeTodos" :key="todo.id" :todo="todo"></TodoView>
      <div
        v-if="todos.length > 3"
        class="card some-more"
      >There are more todos in this note. Go to edit page to see them!</div>
      <div v-if="todos.length === 0" class="card some-more">Empty</div>
    </div>


  </div>
</template>

<script>
  import TodoView from "@/components/TodoView.vue";
  import DeleteNoteModal from "@/components/DeleteNoteModal.vue";
  export default {
    name: "NoteView",
    components: { TodoView, DeleteNoteModal },
    data() {
      return {
        todos: this.$store.getters.getTodosOfNote(this.note.id),
        link: `/edit/${this.note.id}`,
        isDeleteModalVisible: false
      };
    },
    props: ["note"],
    computed: {
      firstThreeTodos() {
        return this.todos
          .slice()
          .reverse()
          .slice(0, 3);
      }
    },
    methods: {
      deleteNote() {
        this.isDeleteModalVisible = true;
      },
      closeModal() {
        this.isDeleteModalVisible = false;
      }
    }
  };
</script> 

<style scoped>
  .note-actions {
    margin-bottom: 1rem;
  }
  .note-title {
    margin-bottom: 1rem;
    margin-top: 1rem;
    font-size: 1.5rem;
    color: green;
    display: flex;
    justify-content: center;
    align-items: center
  }
  .note-view-todo-list {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .some-more {
    display: flex;
    justify-content: center;
    background-color: white;
    border: 1px solid green;
    color: green;
  }
</style>