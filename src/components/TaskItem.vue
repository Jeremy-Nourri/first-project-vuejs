<script setup>

import { ref, watch } from 'vue';

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

// const emitUpdateTask = () => {
//     emit('update-task', { text: updatedText.value });
//     isUpdateInputVisible.value = false;
//     console.log(updatedText.value);
// };

const emitUpdateTask = () => {
    emit('update-task', { text: updatedText });
    isUpdateInputVisible.value = false;
    console.log(updatedText.value);
};

const emitRemoveTask = () => {
  emit('remove-task', props.index);
};

watch(() => props.task, () => {
   updatedText.value.text = props.task.text;
});


</script>

<template>
  <div>
    <li class="task">
      <input v-if="isUpdateInputVisible" v-model.trim="updatedText" />
      <p v-else>{{ props.task.text }}</p>

      <button @click="emitRemoveTask">Supprimer</button>
      
      <button v-if="isUpdateInputVisible" @click="emitUpdateTask">Valider</button>
      <button v-else @click="toggleUpdateInput">Modifier</button>
    </li>

  </div>
</template>

<style>

.task {
  display: flex;
  justify-content: space-around;
  width: 300px;
  margin-top: 0.5rem;
}

p {
  margin: 0;
}

</style>