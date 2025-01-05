<script setup>
import { ref, onMounted } from 'vue';

const name = ref('John Doe');
const status = ref('active');
const tasks = ref(['Task One', 'Task Two', 'Task Three', 'Task Four']);
const link = ref('https://google.com');
const newTask = ref('');

const toggleStatus = () => {
  if (status.value === 'active') {
    status.value = 'pending';
  } else if (status.value === 'pending') {
    status.value = 'inactive';
  } else {
    status.value = 'active';
  }
};

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value);
    newTask.value = ''; // Clear input after adding task
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

onMounted (async () => {
    try {
        const response = await fetch ('https://jsonplaceholder.typicode.com/todos');
        const data = await response.json();
        tasks.value = data.map((task) => task.title);
    } catch {
        console.log('Error fetching tasks');
    }
});
</script>

<template>
  <div>
    <h1>{{ name }}</h1>

    <p v-if="status === 'active'">User is Active</p>
    <p v-else-if="status === 'pending'">
      User is Pending
    </p>
    <p v-else>User is Inactive</p>

    <button @click="toggleStatus">
      Change Status
    </button>

    <form @submit.prevent="addTask">
      <label for="newTask">Add New Task: </label>
      <input
        type="text"
        id="newTask"
        v-model="newTask"
      />
      <button type="submit">
        Add Task
      </button>
    </form>

    <h3>Tasks:</h3>

    <ul>
      <li v-for="(task, index) in tasks" :key="task">
        <span>
            {{ task + ' ' }}
        </span>

        <button @click="deleteTask(index)">
            x
        </button>
      </li>
    </ul>

    <a v-bind:href="link">Link to Google</a>
  </div>
</template>