<template>
  <ul>
    <list-item 
      v-for="(todo, index) in todos"
      :todo="todo"
      v-on:onComplete="onComplete(index)"
      v-on:onDelete="onDelete(index)" />
  </ul>
</template>

<script>
import ListItem from './ListItem'

  export default {
    name: 'list',
    components: {
      ListItem,
    },
    props: ['todos'],
    methods: {
      onComplete: function(index) {
        this.$emit('onCompleteTodo', index);
      },
      onDelete: function(index) {
        this.$emit('onDeleteTodo', index)
      }
    }
  }
</script>