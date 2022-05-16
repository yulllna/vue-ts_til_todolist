<template>
  <div class="button-wrap">
    <button class="active">전체</button>
    <button>처리중</button>
    <button>완료</button>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.button-wrap {
  width: 70%;
  height: 2.5rem;
  display: flex;
  justify-content: space-between;
  margin: 0 auto;
}
button {
  font-size: 1.25rem;
  background: #eee;
  border-radius: 8px;
}
</style>
