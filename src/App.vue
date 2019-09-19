<template>
  <div id="app">
    <Navbar />
    <router-view />
  </div>
</template>

<script>
import Navbar from "./components/Navbar";

export default {
  name: "app",
  components: {
    Navbar
  }
};
</script>

<style>
*,
*::before,
*::after {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  scroll-behavior: smooth;
}
body {
  font-family: "Open Sans", sans-serif;
  color: rgb(34, 34, 34);
  font-size: 16px;
}
input,
button {
  border: none;
  outline: none;
}
button {
  cursor: pointer;
  text-decoration: none;
  padding: 5px;
  border-radius: 5px;
  transition-duration: 0.3s;
  font-family: "Open Sans", sans-serif;
}
.noselect {
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
ul {
  list-style: none;
}
a {
  text-decoration: none;
  cursor: pointer;
  color: rgb(34, 34, 34);
  transition-duration: 0.4s;
}
</style>