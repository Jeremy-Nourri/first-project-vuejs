<script setup>

import TaskItem from "./TaskItem.vue";
import InputAddTask from './InputAddTask.vue';

import { ref } from 'vue';


const tasks = ref([]);

const addTask = newTaskText => {
  tasks.value.push({text: newTaskText})
}

const removeTask = index => {
  tasks.value.splice(index, 1);
}

const updateTask = (index, updatedTask) => {
  tasks.value[index].text = updatedTask;
  console.log(`task 0 ${tasks.value[0].text}`);
}

</script>

<template>
    <InputAddTask @add-task="addTask" />
  <h3 v-if="tasks.length" > Liste des tâches : </h3>
  <ul>

    <TaskItem v-for="(task, index) in tasks"
      :key="index"
      :task="task"
      :index="index"
      @remove-task="removeTask"
      @update-task="updateTask"
    />

  </ul>

</template>

<style>

</style>
