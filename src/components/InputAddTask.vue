<script setup>

import { ref } from "vue";

const newTaskText = ref('');

const emit = defineEmits(['add-task']);

function emitAddTask() {
    emit('add-task', newTaskText.value);
    newTaskText.value = "";
}

</script>

<template>
    <div class="container__add-task">
        <input type="text" v-model.trim="newTaskText" @keyup.enter="emitAddTask">
        <button @click="emitAddTask">Ajouter une tâche</button>
    </div>

</template>

<style>

.container__add-task {
    width: 300px;
}

</style>
