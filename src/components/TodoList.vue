<template>
  <div>
    <input
      type="text"
      v-model="newTodoMsg"
      @keyup.enter='onCreateTodo'
      placeholder="Whats need to be done?"
      class= "create-todo-input" >
    <list
      :todos="todos"
      v-on:onDeleteTodo="onDeleteTodo" 
      v-on:onCompleteTodo="onCompleteTodo" />
  </div>
</template>

<script>
import List from './List'

  export default {
    name: 'todo-list',
    components: {
      List,
    },
    data() {
      return {
        newTodoMsg: '',
        todos: [
          {
            message: 'this is a test message',
            isDone: false,
          }
        ]
      }
    },
    methods: {
      onCreateTodo: function() {
        if (this.newTodoMsg !== '') {
          let objTodo = {
            message: this.newTodoMsg,
            isDone: false,
          }

          this.todos.push(objTodo);
          this.newTodoMsg = '';
        }
      },
      onDeleteTodo: function(index) {
        this.todos.splice(index, 1);
      },
      onCompleteTodo: function(index) {
        this.todos[index].isDone = true;
      }
    }
  }
</script>

<style scoped>
  .create-todo-input {
    padding: 30px 10px 30px 40px;
    width: 700px;
    color: gray;
    font-size: 25px;
    outline: none;
    border: none;
    background: rgba(0, 0, 0, 0.003);
    -webkit-box-shadow: 0px 16px 30px -7px rgba(0,0,0,0.31);
    -moz-box-shadow: 0px 16px 30px -7px rgba(0,0,0,0.31);
    box-shadow: 0px 16px 30px -7px rgba(0,0,0,0.31);

  }
</style>