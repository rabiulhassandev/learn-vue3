<!-- Composition API -->
<script setup>
  import {ref, onMounted} from 'vue';

  const name = ref("Rabiul Hassan");
  const status = ref('active');
  const tasks = ref(['Task 1', 'Task 2', 'Task 3']);
  const taskName = ref('');

  // change the status 
  const changeStatus = () => {
    if(status.value == 'active') status.value = 'inactive'
    else if(status.value == 'inactive') status.value = 'pending'
    else status.value = 'active'
  };

  // add task 
  const AddTask = () => {
    if(taskName.value.trim() == '') return false;

    tasks.value.push(taskName.value);
    taskName.value = '';
  }

  // remove task 
  const removeTask = (index) => {
    tasks.value.splice(index, 1);
  }


  // fetch data from API
  onMounted(async () => {
    try {
      const response = await fetch('https:jsonplaceholder.typicode.com/todos');
      const data = await response.json();
      tasks.value = data.map((task) => task.title);
    } catch (error) {
      console.log("Something Went Wrong!")
    }
  });
</script>


<template>
  <h1>{{ name }}</h1>
  <h1>the status is <b>{{ status }}</b> </h1>

  <form @submit.prevent="AddTask">
    <label for="taskName">Add Task</label>
    <input type="text" id="taskName" name="taskName" v-model="taskName">
    <button type="submit">Submti</button>
  </form>

  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>{{ task }}</span>
      <span><button @click="removeTask(index)">delete</button></span>
    </li>
  </ul>
  <button @click="changeStatus">Change Status</button>

</template>