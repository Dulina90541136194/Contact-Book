<template>
  <div class="contact-list">
    <h2>All Contacts</h2>

    <input
      type="text"
      v-model="search"
      placeholder="Search by name"
    />

    <ul>
      <li
        v-for="contact in filteredContacts"
        :key="contact.id"
      >
        <router-link :to="`/contact/${contact.id}`">
          {{ contact.firstName }} {{ contact.lastName }}
        </router-link>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

const search = ref('')
const contacts = ref([])

onMounted(() => {
  const stored = localStorage.getItem('contacts')
  contacts.value = stored ? JSON.parse(stored) : []
})

const filteredContacts = computed(() => {
  return contacts.value
    .filter(c => {
      const name = `${c.firstName} ${c.lastName}`.toLowerCase()
      return name.includes(search.value.toLowerCase())
    })
    .sort((a, b) => a.lastName.localeCompare(b.lastName))
})
</script>

<style scoped>
.contact-list {
  max-width: 700px;
  margin: 2rem auto;
  padding: 1rem;
}
.contact-list h2 {
  text-align: center;
  margin-bottom: 1rem;
}
input {
  width: 100%;
  padding: 8px;
  margin-bottom: 1rem;
  border: 1px solid #ccc;
  border-radius: 5px;
}
ul {
  list-style: none;
  padding: 0;
}
li {
  margin-bottom: 10px;
}
</style>

