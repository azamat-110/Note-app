<template>
  <div class="modal" @click="$emit('closeModal', false)" v-if="showModal">
    <div class="modal__window" @click.stop>
      <h3 class="modal__window-title">
        {{ edit ? "Изменить заметку" : "Добавить заметку" }}
      </h3>
      <div class="modal__window-inputs">
        <label for="">
          <span>Title</span>
          <input type="text" placeholder="Title" v-model="titleController" />
        </label>
        <label for="">
          <span>Content</span>
          <input type="text" placeholder="Content" v-model="noteController" />
        </label>
      </div>
      <div class="modal__window-btns">
        <button
          class="modal__window-btn del"
          @click="$emit('closeModal', false)"
        >
          <span>Отмена</span>
        </button>
        <button class="modal__window-btn edit" @click="addNote" v-if="!edit">
          <span>Добавить</span>
        </button>
        <button class="modal__window-btn edit" @click="changeNote" v-else>
          <span>Изменить</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      titleController: "",
      noteController: "",
      note: null,
      id: this.currentId,
    };
  },
  props: {
    showModal: Boolean,
    edit: Boolean,
    currentId: Number,
    editedNote: Object,
  },
  methods: {
    addNote() {
      if (this.noteController !== "" && this.titleController !== "") {
        const note = {
          id: this.id++,
          title: this.titleController,
          body: this.noteController,
          date:
            new Date().toLocaleDateString() +
            "  " +
            new Date().toLocaleTimeString(),
        };
        console.log(note);
        this.$emit("addNote", note);
        this.$emit("closeModal", false);
        this.clearController();
      }
    },
    clearController() {
      this.titleController = "";
      this.noteController = "";
    },
    changeNote() {
      if (this.noteController !== "" && this.titleController !== "") {
        const newNoteData = {
          id: this.editedNote.id,
          title: this.titleController,
          body: this.noteController,
          date:
            new Date().toLocaleDateString() +
            "  " +
            new Date().toLocaleTimeString(),
        };
        this.$emit("changeNote", newNoteData);
        this.clearController();
      }
    },
  },
};
</script>

<style>
.modal {
  background: rgba(0, 0, 0, 0.35);
  width: 100%;
  height: 100vh;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal__window {
  background: rgb(243, 237, 247);
  padding: 24px;
  border-radius: 16px;
}

.modal__window-title {
  color: rgb(28, 27, 31);
  font-family: Roboto;
  font-size: 24px;
  font-weight: 400;
  line-height: 32px;
}

.modal__window-inputs label {
  display: flex;
  flex-direction: column;
  border-radius: 4px 4px 0px 0px;
  background: rgb(231, 224, 236);
  padding: 8px 16px;
  gap: 5px;
  border-bottom: 1px solid black;
}

.modal__window-inputs span {
  color: rgb(103, 80, 164);
  font-family: "Roboto";
  font-size: 12px;
  font-weight: 400;
  line-height: 16px;
  letter-spacing: 0.4px;
}
.modal__window-inputs input {
  color: rgb(73, 69, 79);
  font-family: "Roboto";
  font-size: 16px;
  font-weight: 400;
  line-height: 24px;
  letter-spacing: 0.5px;
}
.modal__window-inputs {
  display: flex;
  flex-direction: column;
  gap: 15px;
  padding-top: 16px;
}

.modal__window-btns {
  display: flex;
  gap: 32px;
  padding-top: 24px;
  justify-content: end;
}

.modal__window-btn {
  font-family: "Roboto";
  font-weight: 500;
  line-height: 20px;
  letter-spacing: 0.1px;
  text-align: center;
  text-transform: uppercase;
  font-size: 16px;
  transition: 0.3s;
}

.modal__window-btn:active {
  transform: scale(0.95);
}
</style>