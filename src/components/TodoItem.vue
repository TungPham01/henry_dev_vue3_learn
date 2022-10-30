<template>
  <p  :class="['todoItem', todo.completed ? 'is-completed' : '']">
    <input type="checkbox" :checked="todo.completed" @change="markItemCompleted()" />
    {{ todo.title }}
    <button class="delBtn" @click="handleDeleteItem()">Delete</button>
  </p>
</template>

<script>
// import {ref} from 'vue'

export default {
  name: "TodosItemComponent",
  props: ["todo"],
  setup(props, context) {
    const markItemCompleted = () => {
        context.emit('markCompleted', props.todo.id)
    }
    const handleDeleteItem = () => {
        context.emit('handleDeleteItem', props.todo.id)
    }

    return {
        markItemCompleted,
        handleDeleteItem
    }
  }
};
</script>

<style>
.delBtn {
  background-color: #ff0000;
  color: #fff;
  cursor: pointer;
  float: right;
}

.is-completed {
  text-decoration: line-through;
}

.todoItem {
  background-color: #f4f4f4;
  padding: 10px;
  margin: 0;
  border-bottom: 1px #ccc dotted;
}
</style>