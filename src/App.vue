<template>
  <div id="app">
    <header>
      <TodoHeader />
    </header>
    <main class="todo-container">
      <TodoPasingButtons />
      <TodoInput :item="todoText" @input="updateTodoText" @add="addTodoItem" />
      <TodoList
        :todoItem="todoItems"
        @remove="removeTodoItem"
        @toggle="toggleTodoItemComplete"
      />
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
  save(todoItems: Todo[]) {
    const parsed = JSON.stringify(todoItems);
    localStorage.setItem(STORAGE_KEY, parsed);
  },
  fetch() {
    const todoItems = localStorage.getItem(STORAGE_KEY) || "[]";
    const result = JSON.parse(todoItems);
    return result;
  },
};

export interface Todo {
  title: string;
  done: boolean;
}

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
      todoItems: [] as Todo[],
    };
  },
  methods: {
    updateTodoText(value: string) {
      this.todoText = value;
    },
    addTodoItem() {
      const value = this.todoText;
      const todo: Todo = {
        title: value,
        done: false,
      };
      this.todoItems.push(todo);
      storage.save(this.todoItems);
      // localStorage.setItem(value, value);
      this.initTodoText();
    },
    initTodoText() {
      this.todoText = "";
    },
    fetchTodoItems() {
      this.todoItems = storage.fetch();
    },
    removeTodoItem(index: number) {
      this.todoItems.splice(index, 1);
      storage.save(this.todoItems);
    },
    toggleTodoItemComplete(todoItem: Todo, index: number) {
      this.todoItems.splice(index, 1, {
        ...todoItem[index],
        done: !todoItem[index].done,
      });
      // console.log(todoItem[index].title);
      // console.log(this.todoItems);
      storage.save(this.todoItems);
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
