<template>
  <div class="todo-list">
    <div class="todo-list-head">{{ todoList.listName }}</div>
    <div class="todo-list-main">
      <ul>
        <li>
          <TodoListitem
            v-for="listTodo in todoList.listTodos"
            :key="listTodo.id"
            :todo="listTodo"
            @customChange="changeCheck"
          />
        </li>
      </ul>
    </div>
    <button @click="$emit('deleteTodo', todoList.listId)">delete</button>
    <button @click="$emit('changer', todoList)">edit</button>
  </div>
</template>

<script>
import TodoListitem from "./TodoListitem.vue";
export default {
  components: { TodoListitem },
  props: {
    todoList: {},
  },
  methods: {
    changeCheck(id) {
      this.todoList.listTodos.map((el) => {
        if (el.id === id) {
          el.checked = !el.checked;
        }
      });
    },
  },
};
</script>

<style lang='scss'>
.todo-list {
  & button {
    padding: 10px;
    border: none;
    margin-bottom: 5px;
    &:hover {
      background-color: wheat;
      border: 1px solid black;
    }
  }
  &-head {
    padding: 10px;
    border-radius: 10px;
    background-color: red;
    font-size: 30px;
  }
  border: 1px solid black;
  display: flex;
  margin: 50px;
  padding: 20px;
  flex-direction: column;
  align-items: center;
  width: 200px;
  height: fit-content;
  &-main {
    & ul {
      padding: 0;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
    }
  }
}
ul {
  list-style: none;
}
</style>