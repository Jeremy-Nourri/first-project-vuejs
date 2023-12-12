<script setup>

import InputAddUser from './InputAddUser.vue';
import ContactItem from './ContactItem.vue';

import { ref } from 'vue';

const contacts = ref([]);

const addContact = (newNameText, newEmailText) => {
  contacts.value.push({ name: newNameText, email: newEmailText })
}

const removeContact = index => {
  contacts.value.splice(index, 1);
}

const updateContact = (index, updateNameText, updateEmailText) => {
  contacts.value[index].name = updateNameText;
  contacts.value[index].email = updateEmailText;
}

</script>

<template>
  <InputAddUser @add-contact="addContact" />

  <h3 v-if="contacts.length" >Liste de mes contacts:</h3>

  <ul>
    <ContactItem v-for="(contact, index) in contacts"
      :key="index"
      :name="contact.name"
      :email="contact.email"
      :index="index"
      @remove-contact="removeContact"
      @update-contact="updateContact"
    />
  </ul>

</template>

<style>
ul {
  padding: 0;
}
</style>
