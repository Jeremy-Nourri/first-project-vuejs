<script setup>

import { ref } from "vue";

const newNameText = ref('');
const newEmailText = ref('');

const emit = defineEmits(['add-contact']);

function emitAddContact() {
    emit('add-contact', newNameText.value, newEmailText.value);
    newNameText.value = "";
    newEmailText.value = "";
}

</script>

<template>
    <div class="container__add-task">
        <input required type="text" v-model.trim="newNameText">
        <input required type="email" v-model.trim="newEmailText">
        <button @click="emitAddContact">Ajouter un contact</button>
    </div>
</template>

<style>

.container__add-task {
    width: 300px;
    height: 100px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    margin: auto;
    
    & button {
        width: 100%;
    }
}

</style>
