<script setup>

import { defineProps } from 'vue';

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

</script>

<template>
    <div>
        <li>
            <p>
                {{ props.task.text }}
            </p>
            <div>
            <button @click="$emit('remove-task', props.index)">Remove</button>
            <button @click="$emit('update-task', props.index)">Update</button>
            </div>
        </li>

    </div>
 
</template>

<style>
</style>