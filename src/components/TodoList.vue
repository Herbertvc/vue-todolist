<template>
  <div class="todo-list-container">
    <input
      type="text"
      v-model="newTodoMsg"
      @keyup.enter='onCreateTodo'
      placeholder="Whats need to be done?"
      class= "create-todo-input" >
    <list
      :todos="todosToShow"
      @onDeleteTodo="onDeleteTodo" 
      @onCompleteTodo="onCompleteTodo" />
    <filter-list
      v-show="todos.length > 0"
      :todos="todos"
      @onFilter="onFilter" />
  </div>
</template>

<script>
import List from './List'
import FilterList from './FilterList'
import { filter } from 'lodash/fp'

  export default {
    name: 'todo-list',
    components: {
      List,
      FilterList,
    },
    data() {
      return {
        newTodoMsg: '',
        filterType: '',
        todos: [
          {
            message: 'this is a test message',
            isDone: false,
          }
        ]
      }
    },
    computed: {
      todosToShow: function() {
        let todosFiltered = {};
        switch(this.filterType) {
          case 'ACTIVE':
            todosFiltered = filter(todo => !todo.isDone)(this.todos);
            break;
          case 'COMPLETED':
            todosFiltered = filter(todo => todo.isDone)(this.todos);
            break;
          default:
            todosFiltered = this.todos;
            break;
        }
        return todosFiltered;
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
      },
      onFilter: function(type) {
        this.filterType = type;
      },
    }
  }
</script>

<style scoped>
  .todo-list-container {
    max-width: 700px;
    margin: 0 auto;
  }

  .create-todo-input {
    padding: 30px 10px 30px 40px;
    width: 100%;
    color: gray;
    font-size: 25px;
    outline: none;
    border: none;
    background: white;
    position: relative;
    z-index: 1;
    box-shadow: 0px 9px 30px 1px rgba(0,0,0,0.31);
    -webkit-box-shadow: 0px 9px 30px 1px rgba(0,0,0,0.31);
    -moz-box-shadow: 0px 9px 30px 1px rgba(0,0,0,0.31);
  }
</style>