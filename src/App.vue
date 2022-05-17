<template>
  <div id="app">
    <header>
      <TodoHeader />
    </header>
    <main class="todo-container">
      <TodoPasingButtons />
      <TodoInput :item="todoText" @input="updateTodoText" @add="addTodoItem" />
      <TodoList />
    </main>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import TodoHeader from "./components/TodoHeader.vue";
import TodoPasingButtons from "./components/TodoPasingButtons.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";

const STORAGE_KEY = "vue-ts_todolist";
const storage = {
  save(todoItems: any[]) {
    const parsed = JSON.stringify(todoItems);
    localStorage.setItem(STORAGE_KEY, parsed);
  },
  fetch() {
    const todoItems = localStorage.getItem(STORAGE_KEY) || "[]";
    const result = JSON.parse(todoItems);
    return result;
  },
};

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
      todoItems: [] as any[],
    };
  },
  methods: {
    updateTodoText(value: string) {
      this.todoText = value;
    },
    addTodoItem() {
      const value = this.todoText;
      // this.todoItems.push(value);
      // storage.save(this.todoItems);
      localStorage.setItem(value, value);
      this.initTodoText();
    },
    initTodoText() {
      this.todoText = "";
    },
    fetchTodoItems() {
      this.todoItems = storage.fetch();
    },
  },
  created() {
    this.fetchTodoItems();
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
