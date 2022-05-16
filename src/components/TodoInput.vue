<template>
  <div class="input-wrap">
    <label for="todo-input"></label>
    <input
      id="todo-input"
      type="text"
      placeholder="나의 할 일"
      :value="item"
      class="input-area"
      @input="handleInput"
    />
    <button @click="addTodo" type="button" class="confirm-btn">추가</button>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
// import { VueEvent } from "@/types/index";

export default Vue.extend({
  props: ["item"],
  methods: {
    handleInput(event: any) {
      event.target.value;
    },
    addTodo() {
      console.log("add");
    },
  },
});
</script>

<style>
.input-wrap {
  width: 100%;
  height: 2.5rem;
  display: flex;
  margin: 2% 0 2% 0;
}
.input-area {
  width: 90%;
}
.confirm-btn {
  width: 10%;
}
</style>
