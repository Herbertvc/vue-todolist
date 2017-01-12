<template>
  <div class="todo-list-options">
    <div class="todo-count">{{ todoCount }} items left</div>
    <div class="filters">
      <div class="filter" @click="$emit('onFilter', '')">All</div>
      <div class="filter" @click="$emit('onFilter', 'ACTIVE')">Active</div>
      <div class="filter" @click="$emit('onFilter', 'COMPLETED')">Completed</div>
    </div>
    <div class="todo-clean">Clear complete</div>
  </div>
</template>

<script>
  import { filter } from 'lodash/fp';

  export default {
    name: 'filter-list',
    props: ['todos'],
    computed: {
      todoCount: function() {
        return filter(todo => !todo.isDone)(this.todos).length;
      },
    }
  }
</script>

<style scoped>
  .todo-list-options {
    display: flex;
    justify-content: space-between;
    width: 99.93%;
    background: white;
    padding: 10px 10px 10px 40px;
    position: relative;
    z-index: 2;
    color: #777;
    box-shadow: 0 1px 1px rgba(0, 0, 0, 0.2),
                0 8px 0 -3px #f6f6f6,
                0 9px 1px -3px rgba(0, 0, 0, 0.2),
                0 16px 0 -6px #f6f6f6,
                0 17px 2px -6px rgba(0, 0, 0, 0.2)
  }

  .filters {
    display: flex;
    justify-content: center;
  }

  .filter {
    flex: 0 0 auto;
    border: 1px solid rgba(175, 47, 47, 0.2);
    margin: 0 15px;
    cursor: pointer;
  }
</style>