<script>
export default {
  data() {
    return {
      name: 'John Doe',
      status: 'active',
      tasks: ['Task One', 'Task Two', 'Task Three', 'Task Four'],
      link: 'https://google.com',
    };
  },
  methods: {
    toggleStatus() {
      if (this.status === 'active') {
        this.status = 'pending';
      } else if (this.status === 'pending') {
        this.status = 'inactive';
      } else {
        this.status = 'active';
      }
    },
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