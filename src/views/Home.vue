<template>
  <div class="main">
    <CreateNote />
    <NoteList />
  </div>
</template>

<script>

import CreateNote from '@/components/CreateNote.vue'
import NoteList from '@/components/NoteList.vue'

export default {
  name: 'Home',
  components: {
    CreateNote,
    NoteList
  }
}
</script>

<style scoped>
   .main {
      background-color: rgba(128, 128, 128, 0.479);
      box-shadow: 5px 5px 10px 5px rgba(128, 128, 128, 0.408);  
       }
</style>
