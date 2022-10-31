<template>
  <form @submit.prevent="addItem">
    <input type="text" placeholder="Việc mới..." v-model="title" />
    <input type="submit" value="Thêm" class="addBtn" />
  </form>
</template>

<script>
import { ref } from "vue";
// import { v4 as uuidv4 } from "uuid";
export default {
  name: "addTodoComponent",
  setup(props, context) {
    const title = ref("");
    const addItem = () => {
      const newItem = {
        // id: uuidv4(),
        title: title.value,
        completed: false,
      };
      context.emit("addItem", newItem);
      title.value = "";
    };
    return {
      title,
      addItem,
    };
  },
};
</script>

<style scoped>
form {
  display: flex;
}
input[type="text"] {
  flex: 10;
  padding: 5px;
}
input[type="submit"] {
  flex: 2;
}
</style>