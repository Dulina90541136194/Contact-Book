<template>
  <div v-if="contact" class="details-container">
    <h2>{{ contact.firstName }} {{ contact.lastName }}</h2>
    <p><strong>Email:</strong> {{ contact.email }}</p>

    <router-link :to="`/edit/${contact.id}`">
      <button class="btn">Edit</button>
    </router-link>
    <button @click="deleteContact" class="btn btn-danger">Delete</button>
  </div>
  <div v-else>
    <p>Contact not found.</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'

const route = useRoute()
const router = useRouter()
const contact = ref(null)

onMounted(() => {
  const contacts = JSON.parse(localStorage.getItem('contacts')) || []
  contact.value = contacts.find(c => c.id === route.params.id)
})

function deleteContact() {
  const contacts = JSON.parse(localStorage.getItem('contacts')) || []
  const updated = contacts.filter(c => c.id !== route.params.id)
  localStorage.setItem('contacts', JSON.stringify(updated))
  router.push('/')
}
</script>

<style scoped>
.contact-detail {
  max-width: 600px;
  margin: 2rem auto;
  padding: 1rem;
}
.contact-detail h2 {
  margin-bottom: 1rem;
}
button {
  margin-right: 10px;
}
</style>
