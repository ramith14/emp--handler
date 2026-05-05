<template>
  <div class="nav">
    <router-link to="/">Home</router-link>
    <router-link to="/about">About</router-link>
  </div>
</template>

<script>
export default {
  name: 'NavBar'
}
</script>

<style scoped>
.nav {
  background-color: lightblue;
  padding: 15px;
}

a {
  margin-right: 20px;
  text-decoration: none;
  font-weight: bold;
  color: black;
}

.router-link-exact-active {
  color: red;
}
</style>
