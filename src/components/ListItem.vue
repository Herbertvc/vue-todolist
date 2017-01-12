<template>
  <li v-bind:class="{ 'todo-done': todo.isDone }">
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