// ✅ Step 7: Create Home View (src/views/Home.vue)

<template>
  <div class="search-bar">
    <input type="text" v-model="searchTerm" placeholder="Search by name" />
    <button @click="handleSearch">Enter</button>
  </div>

  <div v-if="filteredContact">
    <h2>{{ filteredContact.lastName }}, {{ filteredContact.firstName }}</h2>
    <p>Email: {{ filteredContact.email }}</p>
    <!-- add more details if needed -->
  </div>
</template>


<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const searchTerm = ref('')
const contacts = ref(JSON.parse(localStorage.getItem('contacts')) || [])
const filteredContact = ref(null)

function handleSearch() {
  filteredContact.value = contacts.value.find(contact =>
    (contact.firstName + ' ' + contact.lastName).toLowerCase().includes(searchTerm.value.toLowerCase())
  )
}
</script>


<style scoped>
.actions {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
}

input {
  padding: 0.5rem;
  width: 60%;
}

button {
  padding: 0.5rem 1rem;
  cursor: pointer;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  margin: 0.5rem 0;
}
</style>
