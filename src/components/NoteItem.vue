<template>
  <div class="note__item">
    <div class="note__item-header" :class="{ between: gridShow }">
      <h3 class="note__item-title">{{ note.title }}</h3>
      <span class="note__item-date">{{ note.date }}</span>
    </div>
    <p class="note__item-descr">
      {{ note.body }}
    </p>
    <div class="note__item-btnsgroup">
      <button class="note__item-btn edit" @click="$emit('changeNote')">
        <img src="../assets/images/edit.svg" alt="" />
        <span>Редактировать</span>
      </button>
      <button class="note__item-btn del" @click="$emit('deleteNote')">
        <img src="../assets/images/delete.svg" alt="" />
        <span>Удалить</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    gridShow: Boolean,
    note: Object,
  },
};
</script>

<style>
.note__item {
  padding: 16px;
  background: rgb(243, 237, 247);
  border-radius: 16px;
  box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15),
    0px 1px 2px 0px rgba(0, 0, 0, 0.3);
}

.note__item-header {
  display: flex;
  flex-direction: column;
}

.note__item-header.between {
  flex-direction: row;
  justify-content: space-between;
}

.note__item-title {
  color: rgb(28, 27, 31);
  font-family: "Roboto";
  font-size: 16px;
  font-weight: 500;
  line-height: 24px;
  letter-spacing: 0.1px;
}

.note__item-date {
  color: rgb(202, 196, 208);
  font-family: "Roboto";
  font-size: 14px;
  font-weight: 400;
  line-height: 20px;
  letter-spacing: 0.25px;
}

.note__item-descr {
  color: rgb(73, 69, 79);
  font-family: "Roboto";
  font-size: 14px;
  font-weight: 100;
  line-height: 20px;
  letter-spacing: 0.25px;
  margin: 16px 0;
}

.note__item-btnsgroup {
  display: flex;
  align-items: center;
  justify-content: right;
  gap: 15px;
  padding: 10px 12px;
}

.note__item-btn {
  display: flex;
  align-items: center;
  gap: 8px;
  font-family: "Roboto";
  font-size: 14px;
  font-weight: 700;
  line-height: 20px;
  letter-spacing: 0.1px;
  text-transform: uppercase;
  transition: 0.3s;
}

.note__item-btn:active {
  transform: scale(0.95);
}

.edit {
  color: rgb(103, 80, 164);
  font-weight: 700;
}

.del {
  color: rgb(207, 27, 27);
  font-weight: 700;
}
</style>
