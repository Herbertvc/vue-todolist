<template>
  <div>
    <ul class="list">
      <list-item 
        v-for="(todo, index) in todos"
        :todo="todo"
        @onComplete="onComplete(index)"
        @onDelete="onDelete(index)" />
    </ul>
  </div>
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

<style scpoped>
  .list {
    width: 100%;
    margin: 0;
    list-style: none;
    padding: 0;
    position: relative;
    z-index: 2;
  }
</style>