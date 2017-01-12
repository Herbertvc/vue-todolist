<template>
  <li class="list-item" :class="{ 'todo-done': todo.isDone }">
    <button @click="completeTodo">complete</button>
    <span>{{ todo.message }}</span>
    <button @click="deleteTodo">delete</button>
  </li>
</template>

<script>
  export default {
    name: 'list-item',
    props: ['todo', 'index'],
    methods: {
      completeTodo: function() {
        this.$emit('onComplete');
      },
      deleteTodo: function() {
        this.$emit('onDelete');
      }
    }
  }
</script>

<style scoped>
  .list-item {
    padding: 30px 10px 30px 40px;
    width: 99.75%;
    border: 1px solid #ededed;
    background: white;
    box-shadow: 0px 14px 30px 1px rgba(0,0,0,0.31);
    -webkit-box-shadow: 0px 14px 30px 1px rgba(0,0,0,0.31);
    -moz-box-shadow: 0px 14px 30px 1px rgba(0,0,0,0.31);
  }

  .todo-done {
    color: red;
    text-decoration: line-through;
  }
</style>