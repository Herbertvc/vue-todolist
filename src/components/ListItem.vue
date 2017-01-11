<template>
  <li class="todo-done">
    <button @click="completeTodo">complete</button>
    <span>{{ todo.message }}</span>
    <button @click="deleteTodo">delete</button>
  </li>
</template>

<script>
  export default {
    name: 'list-item',
    props: ['todo', 'index'],
    data: function() {
      return {
      }
    },
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