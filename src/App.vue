<template>
  <div id="app">
    <TodoHeader />
    <div class="todo-container">
      <TodoPasingButtons />
      <TodoInput :item="todoText" @input="updateTodoText" />
      <TodoList />
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import TodoHeader from "./components/TodoHeader.vue";
import TodoPasingButtons from "./components/TodoPasingButtons.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";

export default Vue.extend({
  components: {
    TodoHeader,
    TodoPasingButtons,
    TodoInput,
    TodoList,
  },
  data() {
    return {
      todoText: "",
    };
  },
  methods: {
    updateTodoText(value: any) {
      this.todoText = value;
    },
  },
});
</script>

<style>
@import "./assets/css/reset.css";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 80vw;
  margin: 5vh auto;
}
.todo-container {
  box-shadow: 1px 1px 10px 3px #e0e0e0;
  padding: 2%;
}
</style>
