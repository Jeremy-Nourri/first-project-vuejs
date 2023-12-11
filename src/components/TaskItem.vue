<script setup>

import { defineProps, ref, watch } from 'vue';

const props = defineProps({
  task: {
    type: String,
    required: true,
  },
  index: {
    type: Number,
    required: true
  }
})

const isUpdateInputVisible = ref(false);

const updatedText = ref(props.task.text);

const toggleUpdateInput = () => {
  isUpdateInputVisible.value = !isUpdateInputVisible.value;
};

const emit = defineEmits(['update-task', 'remove-task',]);

const emitUpdateTask = () => {
    emit('update-task', updatedText.value);
    isUpdateInputVisible.value = false;
};

const emitRemoveTask = () => {
  emit('remove-task', props.index);
};

watch(() => props.task, () => {
  updatedText.value = props.task.text;
});


</script>

<template>
  <div>
    <li>
      <button @click="emitRemoveTask">Supprimer</button>

      <input v-if="isUpdateInputVisible" v-model.trim="updatedText" />
      <p v-else>{{ props.task.text }}</p>
      
      <button v-if="isUpdateInputVisible" @click="emitUpdateTask">Valider</button>
      <button v-else @click="toggleUpdateInput">Modifier</button>
    </li>

  </div>
</template>

<style></style>