<template>
  <AddTodo @addItem="addItem" />
  <TodoItem
    v-for="todo in todos"
    v-bind:key="todo.id"
    v-bind:todo="todo"
    @markCompleted="markCompleted"
    @handleDeleteItem="handleDeleteItem"
  />
</template>

<script>
import { ref } from "vue";
import { v4 as uuidv4 } from "uuid";
import TodoItem from "./TodoItem";
import AddTodo from "./AddTodo";

export default {
  name: "TodosComponent",
  components: {
    TodoItem,
    AddTodo,
  },
  setup() {
    const todos = ref([
      {
        id: uuidv4(),
        title: "Viec 1",
        completed: true,
      },
      {
        id: uuidv4(),
        title: "Viec 2",
        completed: false,
      },
      {
        id: uuidv4(),
        title: "Viec 3",
        completed: false,
      },
    ]);

    const markCompleted = (id) => {
      todos.value = todos.value.map((todo) => {
        if (todo.id == id) {
          todo.completed = !todo.completed;
        }
        return todo;
      });
    };

    const handleDeleteItem = (id) => {
      todos.value = todos.value.filter((todo) => {
        return todo.id !== id;
      });
    };

    const addItem = (event) => {
      todos.value = [...todos.value, event];
    };

    return {
      todos,
      markCompleted,
      handleDeleteItem,
      addItem,
    };
  },
};
</script>

<style>
</style>