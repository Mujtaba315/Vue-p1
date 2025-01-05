<script>
import { ref } from 'vue';

export default {
  setup() {
    const name = ref('John Doe');
    const status = ref('active');
    const tasks = ref(['Task One', 'Task Two', 'Task Three', 'Task Four']);
    const link = ref('https://google.com');

    const toggleStatus = () => {
      if (status.value === 'active') {
        status.value = 'pending';
      } else if (status.value === 'pending') {
        status.value = 'inactive';
      } else {
        status.value = 'active';
      }
    };

    return {
      name,
      status,
      tasks,
      link,
      toggleStatus,
    };
  },
};
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
    <h3>Tasks:</h3>
    <ul>
      <li v-for="task in tasks" :key="task">
        {{ task }}
      </li>
    </ul>
    <a v-bind:href="link">Link to Google</a>
  </div>
</template>