<script setup>

import { ref } from 'vue';

const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  email: {
    type: String,
    required: true,
  },
  index: {
    type: Number,
    required: true
  }
})

const isUpdateInputVisible = ref(false);

const updateNameText = ref(props.name);
const updateEmailText = ref(props.email);

const toggleUpdateInput = () => {
  isUpdateInputVisible.value = !isUpdateInputVisible.value;
};

const emit = defineEmits(['update-contact', 'remove-contact',]);

const emitUpdateContact = () => {
    emit('update-contact', props.index, updateNameText, updateEmailText);
    isUpdateInputVisible.value = false;
};

const emitRemoveContact = () => {
  emit('remove-contact', props.index);
};

</script>

<template>
    <li class="task">
      <input v-if="isUpdateInputVisible" v-model="updateNameText" />
      <p v-else>{{ name }}</p>
      <input v-if="isUpdateInputVisible" v-model="updateEmailText" />
      <p v-else>{{ email }}</p>
      
      <button class="button__validation" v-if="isUpdateInputVisible" @click="emitUpdateContact">✔</button>
      <button v-else @click="toggleUpdateInput">📝</button>
      <button @click="emitRemoveContact">❌</button>
    </li>
</template>

<style>

.task {
  display: flex;
  justify-content: space-around;
  width: 400px;

  & button {
    margin-left: 3px;
  }

  & .button__validation {
    color: green;
  }
}

p {
  margin: 0;
}

</style>