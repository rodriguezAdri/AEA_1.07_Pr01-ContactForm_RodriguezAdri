<template>
  <div>
    <h1>Llibreta de Contactes</h1>
    <form @submit.prevent="addContact">
      <input type="text" v-model="newContact.name" placeholder="Nom" required />
      <input type="tel" v-model="newContact.phone" placeholder="Telèfon" required />
      <button type="submit">Afegir Contacte</button>
    </form>

    <input type="text" v-model="searchContact" placeholder="Cerca per nom" />

    <ul>
      <li v-for="contact in filteredContacts" :key="contact.phone">
        {{ contact.name }} - <a v-bind:href="'tel:' + contact.phone">{{ contact.phone }}</a>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';


const newContact = ref({ name: '', phone: '' });
const contacts = ref([]);
const searchContact = ref('');

const addContact = () => {
  if (newContact.value.name && newContact.value.phone) {
    contacts.value.push({ ...newContact.value });
    newContact.value.name = '';
    newContact.value.phone = '';
  }
};

const filteredContacts = computed(() => {
  return contacts.value.filter(contact =>
    contact.name.toLowerCase().includes(searchContact.value.toLowerCase())
  );
});
</script>

<style scoped>
h1 {
  font-size: 24px;
}
input {
  margin: 5px 0;
}
</style>
