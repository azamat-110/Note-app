<template>
  <div class="container note__list">
    <div class="note__list-header">
      <h2 class="note__list-title" v-if="!search">
        {{ todos.length > 0 ? "Все заметки" : "Нет заметок" }}
      </h2>
      <h2 class="note__list-title" v-else>Поиск</h2>
      <button class="note__list-btn" @click="gridOrList">
        <img
          :src="
            gridShow
              ? require('../assets/images/burger.svg')
              : require('../assets/images/grid.svg')
          "
          alt=""
        />
        <span>{{ gridShow ? "Список" : "Сетка" }}</span>
      </button>
    </div>

    <div class="note__list-items" :class="{ list: gridShow }">
      <NoteItem
        :gridShow="gridShow"
        v-for="todo in todos"
        :key="todo.id"
        :note="todo"
        @openModal="$emit('openModal', true)"
        @deleteNote="$emit('deleteNote', todo.id)"
        @changeNote="$emit('changeNote', todo.id)"
      />
    </div>
  </div>
</template>

<script>
import NoteItem from "./NoteItem.vue";
export default {
  data() {
    return {
      gridShow: false,
    };
  },

  methods: {
    gridOrList() {
      this.gridShow = !this.gridShow;
    },
  },

  components: {
    NoteItem,
  },

  props: {
    todos: Array,
    search: Boolean,
  },
};
</script>

<style>
.note__list {
  margin-top: 30px !important;
}

.note__list-title {
  color: rgb(50, 50, 50);
  font-family: "Roboto";
  font-size: 22px;
  font-weight: 400;
  line-height: 28px;
}

.note__list-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.note__list-btn {
  border-radius: 16px;
  box-shadow: 0px 1px 3px 0px rgba(0, 0, 0, 0.3),
    0px 4px 8px 3px rgba(0, 0, 0, 0.15);
  background: rgb(243, 237, 247);
  padding: 0 20px;
  width: 100%;
  max-width: 121px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  transition: 0.3s;
  height: 56px;
}

.note__list-btn span {
  color: rgb(103, 80, 164);
  font-family: Roboto;
  font-size: 14px;
  font-weight: 700;
  line-height: 20px;
  letter-spacing: 0.1px;
  text-align: center;
}

.note__list-btn:active {
  transform: scale(0.95);
}

.note__list-items {
  margin-top: 30px;
  display: grid;
  gap: 20px;
  grid-template-columns: repeat(3, 1fr);
}

.note__list-items.list {
  grid-template-columns: repeat(1, 1fr);
}
</style>
