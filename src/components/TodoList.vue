<template>
  <div class="todolist-wrap">
    <div class="check-container">
      <div class="check-number">
        <input type="checkbox" />
        <span>n개의 할 일</span>
      </div>
      <div class="check-btns">
        <button>v</button>
        <button>삭제</button>
      </div>
    </div>
    <div class="listitem-container">
      <ul>
        <li
          class="listitem"
          v-for="(items, index) in todoItem"
          :key="index"
          index="index"
        >
          <input type="checkbox" />
          <span class="item-title complete" @click="toggleItem(index)">{{
            `${todoItem[index].title}, ${todoItem[index].done}`
          }}</span>
          <button @click="removeItem(index)">삭제</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script lang="ts">
import { Todo } from "@/App.vue";
import Vue, { PropType } from "vue";

export default Vue.extend({
  props: {
    todoItem: Object as PropType<Todo>,
  },
  methods: {
    removeItem(index: number) {
      this.$emit("remove", index);
    },
    toggleItem(index: number) {
      this.$emit("toggle", this.todoItem, index);
      // console.log(this.todoItem);
      // 데이터 값이 이상하게 저장됌.... 오류수정필
    },
  },
});
</script>

<style scoped></style>

<style scoped>
.todolist-wrap {
  width: 100%;
}
.check-container {
  height: 2.5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.check-number,
.check-btns {
  display: flex;
}
.listitem-container {
  height: auto;
}
.listitem {
  display: flex;
  height: 2.5rem;
  justify-content: space-between;
  align-items: center;
  border: 1px solid #e0e0e0;
}
.item-title {
  cursor: pointer;
}
.item-title.complete {
  text-decoration: line-through;
}
</style>
