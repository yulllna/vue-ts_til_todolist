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
        <li class="listitem" v-for="(items, index) in todoItem" :key="index">
          <input type="checkbox" />
          <span>{{ todoItem[index] }}</span>
          <button @click="removeItem(index)">삭제</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  // data() {
  //   return {
  //     index: index,
  //   };
  // },
  props: {
    todoItem: {
      type: Array,
      required: true,
    },
  },
  methods: {
    removeItem(index: number) {
      this.$emit("remove", index);
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
</style>
