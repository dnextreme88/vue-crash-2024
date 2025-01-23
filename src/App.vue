<script setup>
  import { ref } from 'vue';

  // ref is basically setting the initial state of the data
  // Use ref('') for blank values
  const name = ref('John Doe');
  const status = ref('active');
  const tasks = ref(['Task One', 'Task Two']);
  const newTask = ref('');

  const toggleStatus = () => {
    if (status.value === 'active') {
      status.value = 'pending';
    } else if (status.value === 'pending') {
      status.value = 'inactive';
    } else {
      status.value = 'active';
    }
  }

  const addTask = () => {
    if (newTask.value.trim() !== '') {
      tasks.value.push(newTask.value); // Add to array
      newTask.value = ''; // Set it back to blank
    }
  }
</script>

<template>
  <h1>Vue Jobs</h1>

  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else="status === 'inactive'">User is inactive</p>

  <button @click="toggleStatus">Change Status</button>

  <!-- .prevent is basically adding e.preventDefault() from vanilla JS -->
  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>

  <ul>
    <li v-for="(task, index) in tasks" :key="task">{{ task }}</li>
  </ul>
</template>

<!-- scoped means that the styles only apply to this component -->
<style scoped>
  h1 {
    color: red;
  }
</style>
