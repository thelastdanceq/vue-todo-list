<template>
  <div class="changer">
    <div class="changer-bc">
      <div class="changer-modal">
        <input
          class="changer-modal-list-title"
          type="text"
          :value="list.listName"
          @input="
            (e) =>
              $emit(
                'editTodo',
                { ...list, listName: e.target.value },
                list.listId
              )
          "
        />
        <div class="changer-modal-list-todos-titles">
          <input
            v-for="todo in list.listTodos"
            v-bind:key="todo.id"
            type="text"
            :value="todo.todoTitle"
            @input="(e) => hanlder(e, todo.id)"
          />
          <div
            class="changer-modal-add-new btn"
            @click="$emit('addNewTodo', list.listId)"
          >
            +
          </div>
          <div class="changer-modal-save btn" @click="$emit('changer', {})">
            close
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    list: {},
  },
  methods: {
    hanlder(e, id) {
      this.list.listTodos.forEach((el) => {
        if (el.id === id) {
          el.todoTitle = e.target.value;
        }
      });
      this.$emit("editTodo", { ...this.list }, this.list.listId);
    },
  },
};
</script>

<style lang="scss" scoped>
.changer-bc {
  //opacity: 0.3;
  background-color: wheat;
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
  position: fixed;
}

.btn {
  width: 318px;
  height: 45px;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 0 0 5px 0;
  margin: 30px;
  background-color: red;
}
.changer-modal {
  color: black;
  font-size: 80px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.changer-modal-list-title {
  margin: 30px;
  font-size: 34px;
}
.changer-modal-list-todos-titles {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  & input {
    font-size: 25px;
    margin-bottom: 30px;
  }
}
</style>
