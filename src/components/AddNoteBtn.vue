<template>
  <div>
    <button class="add__note-btn" @click="$emit('openModal', true)">
      <img :src="require('@/assets/images/edit.svg')" alt="" />
    </button>
  </div>
</template>

<script>
export default {};
</script>

<style>
.add__note-btn {
  border-radius: 16px;
  box-shadow: 0px 1px 3px 0px rgba(0, 0, 0, 0.3),
    0px 4px 8px 3px rgba(0, 0, 0, 0.15);
    background: rgb(243, 237, 247);
  width: 56px;
  height: 56px;
  position: fixed;
  bottom: 30px;
  right: 30px;
  transition: .3s;
}

.add__note-btn:active{
    transform: scale(.95);
}
</style>