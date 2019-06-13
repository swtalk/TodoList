<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <todo-input @addTodo="appAddTodo"></todo-input>
    <todo-list v-bind:propsdata="todoItems" @removeTodo="appRemoveTodo"></todo-list>
    <todo-footer @removeAll="appClearAll"></todo-footer>
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoFooter from "./components/TodoFooter.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";

export default {
  data() {
    return {
      todoItems: []
    };
  },

  methods: {
    appAddTodo(todoItem) {
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    appClearAll() {
      localStorage.clear();
      this.todoItems = [];
    },
    appRemoveTodo(todoItem, index) {
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index, 1);
    }
  },
  components: {
    TodoHeader: TodoHeader,
    TodoFooter: TodoFooter,
    TodoInput: TodoInput,
    TodoList: TodoList
  },
  created() {
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        this.todoItems.push(localStorage.key(i));
      }
    }
  }
};
</script>









<style>
body {
  text-align: center;
  background-color: #f6f6f6;
}
input {
  border-style: groove;
  width: 200px;
}
button {
  border-style: groove;
}
.showdow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>

