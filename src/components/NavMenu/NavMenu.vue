<!-- NavMenu.vue -->
<template>
  <nav class="menu">
    <ul class="menu__list">
      <li class="menu__item" @click="handleClick('home')" :class="{ 'menu__item--active': activeItem === 'home' }">
        <a href="#" class="menu__link">Главная</a>
      </li>
      <li class="menu__item" @click="handleClick('about')" :class="{ 'menu__item--active': activeItem === 'about' }">
        <a href="#" class="menu__link">О нас</a>
      </li>
      <li class="menu__item" @click="handleClick('todoList')" :class="{ 'menu__item--active': activeItem === 'todoList' }">
        <a href="#" class="menu__link">To-Do List</a>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  props: {
    activeItem: {
      type: String,
      required: true,
    },
  },
  methods: {
    handleClick(item) {
      this.$emit("menuClick", item);
    },
  },
};
</script>


<style lang="scss">
@import "./NavMenu.scss";
</style>
