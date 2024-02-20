<template>
  <div id="nav">
    <router-link :to="{ path: '/' }">
      <img src="" alt="" id="logo" />
    </router-link>
    <router-link to="/">Home</router-link> |
    <router-link to="/orders">Pedidos</router-link>
  </div>
</template>

<script>
export default {
  name: "Navbar-html",
};
</script>

<style scoped></style>
