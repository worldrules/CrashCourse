<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div>
    <div v-bind:key="todo.id" v-for="todo in todos">
      <TodoItem
        v-bind:todo="todo"
        @mark-complete="handleMarkComplete"
        v-on:del-todo="$emit('del-todo', todo.id)"
      />
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Todos",
  components: { TodoItem },
  props: ["todos"],
  methods: {
    handleMarkComplete(todoId) {
      const todoIndex = this.todos.findIndex((todo) => todo.id === todoId);
      if (todoIndex !== -1) {
        // Create a new object to avoid modifying the original array directly
        const updatedTodo = { ...this.todos[todoIndex] };
        updatedTodo.completed = !updatedTodo.completed;

        // Update the array with the new todo object
        this.$set(this.todos, todoIndex, updatedTodo);
      }
    },
  },
};
</script>

<style scoped>
</style>