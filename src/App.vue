<template>
  <div id="app">
    <nav>
      <router-link to="/home">Home</router-link> |
      <router-link to="/stats">Stats</router-link> |
      <router-link to="/login" v-if="!loggedIn">Login</router-link>
      <router-link to="/logout" v-if="loggedIn">Logout</router-link>
    </nav>
    <router-view />
  </div>
</template>

<style>
nav {
  text-align: center;
  padding-top: 20px;
}
a {
  text-decoration: none;
  color: #000;
  font-size: 25px;
  padding: 10px;
}
</style>

<script>
export default {
  data() {
    return {
      loggedIn: false,
    };
  },
};
</script>
