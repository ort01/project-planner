<template>
  <nav class="main-nav">
    <router-link to="/">Projects</router-link> |
    <router-link :to="{ name: 'AddProject' }">Add a New Project</router-link>
  </nav>
</template>

<script>
export default {};
</script>

<style>
.main-nav {
  text-align: center;
  margin: 40px auto;
}
.main-nav a {
  display: inline-block;
  text-decoration: none;
  font-size: 18px;
  color: #999;
  margin: 0 10px;
}

a.router-link-active {
  border-bottom: 2px solid rgba(69, 148, 69, 0.521);
  color: rgb(87, 87, 87);
}
</style>