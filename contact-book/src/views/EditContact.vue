<template>
  <div class="edit-contact">
    <h2>Edit Contact</h2>
    <form @submit.prevent="updateContact">
      <div>
        <label for="firstName">First Name:</label>
        <input id="firstName" v-model="contact.firstName" required />
      </div>
      <div>
        <label for="lastName">Last Name:</label>
        <input id="lastName" v-model="contact.lastName" required />
      </div>
      <div>
        <label for="email">Email:</label>
        <input id="email" type="email" v-model="contact.email" required />
      </div>
      <button type="submit">Save Changes</button>
    </form>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRouter, useRoute } from 'vue-router'

const contact = ref({})
const route = useRoute()
const router = useRouter()
const contactId = route.params.id

onMounted(() => {
  const contacts = JSON.parse(localStorage.getItem('contacts')) || []
  const existingContact = contacts.find(c => c.id === contactId)
  if (!existingContact) {
    alert('Contact not found')
    router.push('/')
  } else {
    contact.value = { ...existingContact }
  }
})

function updateContact() {
  const contacts = JSON.parse(localStorage.getItem('contacts')) || []
  const index = contacts.findIndex(c => c.id === contactId)
  if (index !== -1) {
    contacts[index] = contact.value
    localStorage.setItem('contacts', JSON.stringify(contacts))
    router.push(`/contact/${contactId}`)
  }
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
