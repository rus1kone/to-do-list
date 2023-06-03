<!-- App.vue -->
<template>
  <div id="app">
    <NavMenu :activeItem="activeItem" @menuClick="handleMenuClick" />
    <div v-if="activeItem === 'home'">
      <HomePage />
    </div>

    <div v-if="activeItem === 'about'">
      <AboutPage />
    </div>

    <div v-if="activeItem === 'todoList'">
      <TodoList />
    </div>
  </div>
</template>

<script>
import NavMenu from "./components/NavMenu/NavMenu.vue";
import HomePage from "./components/HomePage/HomePage.vue";
import AboutPage from "./components/AboutPage/AboutPage.vue";
import TodoList from "./components/TodoList/TodoList.vue";

export default {
  name: "App",
  components: {
    NavMenu,
    HomePage,
    AboutPage,
    TodoList,
  },
  data() {
    return {
      activeItem: "home",
    };
  },
  methods: {
    handleMenuClick(item) {
      this.activeItem = item;
    },
  },
};
</script>


<style lang="scss">
@import "@/styles/main.scss";
</style>
