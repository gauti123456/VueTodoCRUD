<template>
  <div>
    <div v-bind:key="todo.id" v-for="todo in todos">
      <TodoItem v-bind:id="todo.id" v-bind:title="todo.title"
       v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)"
       v-bind:todos="todos"/>
    </div>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue';
export default {
  name: "Todos",
  components: {
    TodoItem
  },
  props: ["todos"]
}
</script>

<style scoped>
</style>