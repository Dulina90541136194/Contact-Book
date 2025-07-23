<template>
  <div class="add-contact">
    <h2>Add New Contact</h2>
    <form @submit.prevent="saveContact">
      <label>First Name:</label>
      <input v-model="firstName" required />

      <label>Last Name:</label>
      <input v-model="lastName" required />

      <label>Email:</label>
      <input v-model="email" type="email" required />

      <button type="submit">Add Contact</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { v4 as uuidv4 } from 'uuid'

const firstName = ref('')
const lastName = ref('')
const email = ref('')
const router = useRouter()

function saveContact() {
  const newContact = {
    id: uuidv4(),
    firstName: firstName.value,
    lastName: lastName.value,
    email: email.value
  }

  const existingContacts = JSON.parse(localStorage.getItem('contacts')) || []
  existingContacts.push(newContact)
  localStorage.setItem('contacts', JSON.stringify(existingContacts))

  router.push(`/contact/${newContact.id}`)
}
</script>

<style scoped>
form {
  max-width: 500px;
  margin: 2rem auto;
  display: flex;
  flex-direction: column;
}
input {
  margin-bottom: 1rem;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
}
button {
  padding: 10px;
  background-color: #2196F3;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
button:hover {
  background-color: #1976D2;
}
</style>
