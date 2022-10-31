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
// import { v4 as uuidv4 } from "uuid";
import axios from "axios";
import TodoItem from "./TodoItem";
import AddTodo from "./AddTodo";

export default {
  name: "TodosComponent",
  components: {
    TodoItem,
    AddTodo,
  },
  setup() {
    const todos = ref([]);

    const getAllTodos = async () => {
      try {
        const res = await axios.get(
          "https://jsonplaceholder.typicode.com/todos?_limit=5"
        );
        todos.value = res.data;
      } catch (e) {
        console.log(e);
      }
    };
    getAllTodos();

    const markCompleted = (id) => {
      todos.value = todos.value.map((todo) => {
        if (todo.id == id) {
          todo.completed = !todo.completed;
        }
        return todo;
      });
    };

    const handleDeleteItem = async (id) => {
      try {
        await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`);
        todos.value = todos.value.filter((todo) => {
          return todo.id !== id;
        });
      } catch (e) {
        console.log(e);
      }
    };

    const addItem = async (event) => {
      try {
        await axios.post(`https://jsonplaceholder.typicode.com/todos`, event);
        todos.value = [...todos.value, event];
      } catch (e) {
        console.log(e);
      }
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