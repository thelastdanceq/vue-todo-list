<template>
  <div id="app">
    <ChangerModal
      v-if="Object.keys(changer).length > 0"
      :list="changer"
      @editTodo="editTodo"
      @changer="changerSwitch"
      @addNewTodo="addNewTodo"
    />
    <h2>
      {{
        "You `ve done " +
        this.list.reduce((prev, todoList) => {
          return (
            prev +
            todoList.listTodos.reduce((prev2, todoRow) => {
              if (todoRow.checked) {
                return prev2 + 1;
              }
              return prev2;
            }, 0)
          );
        }, 0) +
        " todos!"
      }}
    </h2>
    <div class="todo-lists">
      <AddNewTodo @addnew="addNewTodoList" />
      <TodoList
        v-for="todolist in list"
        v-bind:key="todolist.id"
        v-bind:todoList="todolist"
        @deleteTodo="deleteTodo"
        @changer="changerSwitch"
      />
    </div>
  </div>
</template>

<script>
import AddNewTodo from "./components/AddNewTodo.vue";
import ChangerModal from "./components/ChangerModal.vue";
import TodoList from "./components/TodoList.vue";
export default {
  name: "App",
  components: { TodoList, AddNewTodo, ChangerModal },
  data() {
    return {
      list: [
        {
          listId: 1,
          listName: "Companies",
          listTodos: [
            { id: 1, todoTitle: "Microsoft", checked: false },
            { id: 2, todoTitle: "Apple", checked: false },
            { id: 3, todoTitle: "Nestle", checked: false },
          ],
        },
        {
          listId: 2,
          listName: "privet",
          listTodos: [
            { id: 1, todoTitle: "Nike", checked: false },
            { id: 2, todoTitle: "Gucci", checked: false },
            { id: 3, todoTitle: "Versache", checked: false },
          ],
        },
      ],

      changer: {},
    };
  },
  methods: {
    changerSwitch(data) {
      this.changer = data;
    },
    addNewTodoList() {
      this.list = [
        ...this.list,
        {
          listId: Date.now(),
          listName: "None",
          listTodos: [{ id: 1, todoTitle: "None", checked: false }],
        },
      ];
    },
    deleteTodo(id) {
      this.list = this.list.filter((el) => {
        return el.listId !== id;
      });
    },
    editTodo(data, id) {
      const index = this.list.findIndex((el) => {
        return el.listId == id;
      });
      this.list[index] = Object.assign(this.list[index], { ...data });
    },
    addNewTodo(id) {
      const index = this.list.findIndex((el) => {
        return el.listId == id;
      });

      this.list[index].listTodos = [
        ...this.list[index].listTodos,
        {
          id: Date.now(),
          checked: false,
          todoTitle: "none",
        },
      ];
    },
  },
};
</script>

<style lang='scss' rel="stylesheet/scss">
#app {
  & .todo-lists {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
  }
}
</style>
