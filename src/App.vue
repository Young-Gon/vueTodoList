<template>
  <div id="app">
    <todo-header/>
    <todo-input @addTodo="addTodo"/>
    <todo-list v-bind:propsdata="todoItems" @removeTodo="removeTodo"/>
    <todo-footer @removeAll="clearAll"/>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'
export default {
  name: 'app',
  components:{
    'TodoHeader': TodoHeader,
    'TodoInput': TodoInput,
    'TodoList': TodoList,
    'TodoFooter': TodoFooter,
  },
  data() {
    return {
      todoItems: []
    }
  },
  created() {
    if (localStorage.length > 0) {
      for (let i =0; i< localStorage.length;i++) {
        this.todoItems.push(localStorage.key(i));
      }
    }
  },
  methods: {
    addTodo(todoItem) {
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    removeTodo(todoItem, index) {
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index, 1);
    },
    clearAll() {
      localStorage.clear();
      this.todoItems = [];
    }
  }
}
</script>

<style>
  @import url('https://use.fontawesome.com/releases/v5.6.3/css/all.css');

  body {
   text-align: center;
   background-color: #F6F6F8;
  }
  input {
    border-style: groove;
    width: 200px;
  }
  button {
    border-style: groove;
  }
  .shadow{
    box-shadow: 5px 10px 10px rgba(0,0,0,0.03);
  }
</style>
