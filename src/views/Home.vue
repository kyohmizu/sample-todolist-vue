<template>
  <div class="home">
    <todo-list></todo-list>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import TodoList from '@/components/TodoList.vue';

export default Vue.extend({
  name: 'home',
  components: {
    TodoList,
  },
});
</script>
