<template>
  <div id="app">
    <v-toolbar title="Task Manager"></v-toolbar>
    <v-container>
      <TodoApp />
    </v-container>

  </div>
</template>

<script>
import TodoApp from './components/TodoApp.vue';

export default {
  components: {
    TodoApp
  }
};
</script>
