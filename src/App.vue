<template>
  <div class="wrapper">
    <NavBar @showSearchBar="showSearchBar" @seachValue="search = $event" />
    <NoteList
      :todos="filterNotes"
      :search="showSearch"
      @openModal="openEditModal"
      @deleteNote="deleteNote"
      @changeNote="changeNoteData"
    />
    <ModalWin
      :showModal="showModal"
      @closeModal="closeModal"
      :edit="edit"
      :currentId="currentId"
      @addNote="addNote"
      :editedNote="editedNote"
      @changeNote="editNoteData"
    />
    <AddNoteBtn @openModal="openModal" />
  </div>
</template>

<script>
import NavBar from "./components/NavBar.vue";
import NoteList from "./components/NoteList.vue";
import AddNoteBtn from "./components/AddNoteBtn.vue";
import ModalWin from "@/components/ModalWin.vue";
export default {
  data() {
    return {
      currentId: 1,
      todos: [],
      showSearch: false,
      showModal: false,
      edit: false,
      editedNote: {},
      search: "",
    };
  },

  components: {
    NavBar,
    NoteList,
    AddNoteBtn,
    ModalWin,
  },

  methods: {
    showSearchBar(showSearch) {
      this.showSearch = showSearch;
    },
    openModal(status) {
      this.edit = false;
      this.showModal = status;
    },
    openEditModal() {
      this.edit = true;
      this.showModal = true;
    },
    closeModal(status) {
      this.showModal = status;
    },
    addNote(note) {
      this.todos.push(note);
    },
    deleteNote(id) {
      const index = this.todos.findIndex((note) => note.id == id);
      this.todos.splice(index, 1);
    },
    getNotes() {
      const localNotes = localStorage.notes;
      if (localNotes) {
        this.todos = JSON.parse(localNotes);
        this.currentId = this.todos.length;
        this.currentId++;
      }
    },
    changeNoteData(id) {
      this.openEditModal();
      let pickedNote = this.todos.find((note) => note.id == id);
      this.editedNote = pickedNote;    
    },
    editNoteData(newNoteData) {
      this.todos.forEach((note) => {
        if (note.id == newNoteData.id) {
          note.title = newNoteData.title;
          note.body = newNoteData.body;
          note.date = newNoteData.date;
        }
      });
      this.closeModal();
    },
  },

  watch: {
    todos: {
      handler(newNotes) {
        localStorage.notes = JSON.stringify(this.todos);
      },
      deep: true,
    },
  },
  created() {
    this.getNotes();
  },
  computed: {
    filterNotes() {
      return this.search
        ? this.todos.filter((todo) =>
            todo.title.toLowerCase().includes(this.search.toLowerCase())
          )
        : this.todos;
    },
  },
  provide:{

  }
};
</script>

<style>
</style>