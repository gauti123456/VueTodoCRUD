<template>
  <div class="container">
    <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
      <p>
        <input type="checkbox" v-on:change="markComplete" v-bind:checked="todo.completed" />
        {{todo.title}}
        <button class="update" @click="updateTodo">Update</button>
        <button @click="$emit('del-todo', todo.id)" class="del">x</button>
      </p>
    </div>
    <div v-if="this.flag">
      <form @submit="updateTodoMethod">
        <div class="form-group">
          <input
            class="form-control"
            v-model="updateTitle"
            type="text"
            :placeholder="title"
            name
            id
          />
        </div>
        <div class="form-group">
          <button class="btn btn-danger">Update</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo", "todos", "title", "id"],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
    },
    updateTodo() {
      this.flag = !this.flag;
    },
    updateTodoMethod(e) {
      e.preventDefault();
      console.log(this.title);
      console.log(this.id);
      this.todos.filter((todo) => {
        if (todo.id == this.id) {
          todo.title = this.updateTitle;
        }
      });
      this.flag = false
    },
  },
  data() {
    return {
      flag: false,
      updateTitle: "",
    };
  },
};
</script>

<style scoped>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  margin: 20px;
  border-bottom: 1px #ccc dotted;
}

.is-complete {
  text-decoration: line-through;
}

.del {
  background: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}

.update {
  background: blue;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>
