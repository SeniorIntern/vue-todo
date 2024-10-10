<script setup>
import { ref } from "vue";

let id = 0;

const newTodo = ref("");

const todos = ref([
  {
    id: id++,
    text: "Read Vue Docs",
  },
  {
    id: id++,
    text: "Make todo app",
  },
]);

const handleTaskAdd = () => {
  todos.value.push({
    id: id++,
    text: newTodo.value,
  });
  newTodo.value = "";
};

const handleTaskDelete = (id) => {
  todos.value = todos.value.filter((todo) => todo.id !== id);
};

const handleTaskUpdate = (id) => {
  todos.value[id].text = newTodo.value;
  newTodo.value = "";
};
</script>

<template>
  <section>
    <div class="container">
      <form @submit.prevent="handleTaskAdd" class="todo__form">
        <h1 class="todo__form_header">Best Todo App!</h1>
        <div class="todo__form_field">
          <label for="task">Enter your next task</label>
          <input v-model="newTodo" name="task" id="task" placeholder="Aa" />
        </div>

        <button>Add Task</button>
      </form>

      <ul>
        <li class="list__item" v-for="todo in todos" :key="todo.id">
          <span>{{ todo.text }}</span>
          <div class="list__item__controls">
            <button class="delete_btn" @click="handleTaskDelete(todo.id)">
              Delete
            </button>
            <button class="update_btn" @click="handleTaskUpdate(todo.id)">
              Update
            </button>
          </div>
        </li>
      </ul>
    </div>
  </section>
</template>

<style>
section {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

ul {
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  padding-left: 0;
  gap: 0.4em;
}

input {
  padding: 0.4em 0.8em;
  border-radius: 0.4em;
  border: 0.5px solid black;
}

button {
  cursor: pointer;
  width: fit-content;
  border: 0.5px solid black;
  padding: 0.6em 1.2em;
  border: 0.4em;
  color: white;
  border-radius: 0.4em;
}

form button {
  width: 100%;
  background-color: black;
  margin-left: auto;
  margin-right: auto;
}

.container {
  width: 500px;
  display: grid;
  gap: 1.4em;
  grid-template-columns: repeat(1, 1fr);
}

.list__item {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.list__item__controls {
  display: flex;
  gap: 0.4em;
}

.todo__form {
  background-color: #d7f7f5;
  border-radius: 0.8em;
  padding: 1.4em;
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  gap: 1.2em;
}

.todo__form_header {
  text-align: center;
  font-weight: 400;
}

.todo__form,
.todo__form_field {
  display: grid;
  grid-template-columns: repeat(1, 1fr);
}

.todo__form_field {
  gap: 0.6em;
}

.delete_btn {
  background-color: hsl(0, 100%, 65%);
}

.update_btn {
  background-color: hsl(0, 0%, 80%);
}
</style>
