<template>
  <div id="app">
    <nav>
      <router-link to="/" exact-active-class="active-link">Home</router-link>
      <router-link to="/contacts" exact-active-class="active-link">Contacts</router-link>
      <router-link to="/add" exact-active-class="active-link">Add Contact</router-link>
    </nav>
    <router-view />
  </div>
</template>



<style scoped>
nav {
  background-color: #eee;
  padding: 10px;
}
nav a {
  margin: 0 10px;
  text-decoration: none;
}
</style>
