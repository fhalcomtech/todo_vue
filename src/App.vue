<template>
  <Todo />
</template>

<style lang="scss">
@import "@/assets/styles/todo.scss";

*,
*:before,
*:after {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  background-color: $gunmetal;
  color: $cultured;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>

<script>
import Todo from "@/views/Todo";

export default {
  name: "App",
  components: {
    Todo,
  },
};
</script>
