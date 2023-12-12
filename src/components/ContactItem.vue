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
  <div>
    <li class="task">
      <input v-if="isUpdateInputVisible" v-model="updateNameText" />
      <p v-else>{{ name }}</p>
      <input v-if="isUpdateInputVisible" v-model="updateEmailText" />
      <p v-else>{{ email }}</p>

      <button @click="emitRemoveContact">Supprimer</button>
      
      <button v-if="isUpdateInputVisible" @click="emitUpdateContact">✔</button>
      <button v-else @click="toggleUpdateInput">📝</button>
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