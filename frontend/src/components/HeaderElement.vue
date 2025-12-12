<template>
  <header>
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/contacts">Contacts</router-link>
    </nav>
  </header>
</template>

<script>
export default {
  name: "HeaderElement",
  props: {},
};
</script>

<style>
header {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  padding: 8px;
  background-color: #bfbfbf;
  border-radius: 16px;
  margin: 8px 0;
}

header nav {
  display: flex;
  align-items: center;
}

nav > a {
  display: inline-block;
  padding: 4px 8px;
  margin: 0 4px;
}

nav > a:hover {
  background: lightgrey;
  border-radius: 4px;
}
</style>
