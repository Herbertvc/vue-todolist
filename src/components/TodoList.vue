<template>
  <div>
    <input
      type="text"
      v-model="newTodoMsg"
      @keyup.enter='onCreateTodo'>
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