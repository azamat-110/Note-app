<template>
  <div>
    <nav class="nav">
      <div class="nav__content" v-if="!showSearch">
        <button class="nav__btn">
          <span>RU</span>
        </button>
        <h1 class="nav__title">Заметки</h1>
        <button class="nav__btn" @click="showSearchBar">
          <img src="../assets/images/search.svg" alt="" />
        </button>
      </div>
      <div class="nav__search" v-if="showSearch">
        <button class="nav__btn" @click="showSearchBar">
          <img src="../assets/images/back.svg" alt="" />
        </button>
        <input type="text" placeholder="Поиск..." v-model="searchController" />
        <button @click="clearController" class="nav__btn">
          <img src="../assets/images/x_btn.svg" alt="" />
        </button>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showSearch: false,
      searchController: "",
    };
  },
  methods: {
    showSearchBar() {
      this.showSearch = !this.showSearch;
      this.$emit("showSearchBar", this.showSearch);
    },

    clearController() {
      if (this.searchController.length > 0) {
        this.searchController = "";
        this.$emit("showSearchBar", this.showSearch);
      } else {
        this.showSearchBar();
      }
    },
  },
  watch:{
    searchController(val){
       this.$emit('seachValue', val);
       console.log(val);
    }
  }
};
</script>

<style>
.nav {
  padding: 14px 16px;
  box-shadow: 0px 1px 3px 0px rgba(0, 0, 0, 0.3),
    0px 4px 4px 0px rgba(0, 0, 0, 0.25);
  background: rgb(243, 237, 247);
}

.nav__content,
.nav__search {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.nav__title,
.nav__btn span {
  color: rgb(28, 27, 31);
  font-family: Roboto;
  font-size: 22px;
  font-weight: 400;
  line-height: 28px;
  letter-spacing: 0%;
  text-align: center;
}

.nav__btn {
  transition: 0.5s;
  width: 40px;
  height: 40px;
}

.nav__btn:active {
  transform: scale(0.9);
}

.nav__search input {
  width: 100%;
  max-width: 80%;
  color: rgb(157, 157, 157);
  font-family: Roboto;
  font-size: 16px;
  font-weight: 400;
  line-height: 20px;
}

.nav__search input::placeholder {
  color: rgb(157, 157, 157);
}
</style>