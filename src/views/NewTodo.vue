<template>
  <form @submit.prevent="submitNewTodo">
    <div v-if="errors.length">
      <h3>入力内容にエラーがあります</h3>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }} </li>
      </ul>
    </div>
    <div>
      <label>やること</label>
      <input type="type" v-model="text" />
    </div>
    <div>
      <input type="submit" value="登録" />
    </div>
  </form>
</template>

<script lang="ts">
import Vue from 'vue'
import todoService from "@/services/TodoService";

declare interface NewTodoData {
  errors: string[];
  text: string;
}

export default Vue.extend({
  data() {
    return {
      errors: [],
      text: "",
    } as NewTodoData;
  },
  methods: {
    async submitNewTodo() {
      this.errors = [];
      if (!this.text) {
        this.errors.push("やることを入力してください");
        return;
      }

      await todoService.add({
        id: 0,
        text: this.text,
        done: false,
      });

      this.$router.push({name: "home"});
    }
  }
});
</script>

<style>
ul {
  list-style-type: none;
}
</style>