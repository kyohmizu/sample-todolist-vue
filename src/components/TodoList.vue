<template>
  <div id="todo-list">
    <h1>TODO リスト</h1>
    <p v-if="errorMessage">{{ errorMessage }}</p>
    <ol>
      <li v-for="todo in todos" v-bind:key="todo.id">
        <input type="checkbox" v-model="todo.done" @change="event => todoStatusChanged(todo)" />
        {{ todo.text }}
      </li>
    </ol>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import TodoItem from "@/models/TodoItem";
import todoService from "@/services/TodoService";

declare interface TodoListData {
  todos: TodoItem[];
  errorMessage: string;
}

export default Vue.extend({
  data() {
    return {
      todos: [],
      errorMessage: "",
    } as TodoListData;
  },
  methods: {
    async todoStatusChanged(updatedTodoItem: TodoItem) {
      await todoService.update(updatedTodoItem);
    }
  },
  async created() {
    try {
      this.todos = await todoService.getAll();
    } catch {
      this.errorMessage = "TODO リストの取得中にエラーが発生しました。";
    }
  }
});
</script>

<style>
li {
  list-style-type: none;
}
</style>