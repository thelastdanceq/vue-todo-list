<template>
  <div class="todo-list-item" @click="changer">
    <p>{{ todo.todoTitle }}</p>
    <input type="checkbox" :checked="todo.checked" />
  </div>
</template>

<script>
export default {
  props: {
    todo: {},
  },
  methods: {
    changer() {
      this.$emit("customChange", this.todo.id);
    },
  },
};
</script>

<style lang='scss'>
.todo-list-item {
  display: flex;
  align-items: center;
  & p,
  input {
    flex-grow: 1;
  }
  & p {
    font-size: 20px;
  }
}
</style>