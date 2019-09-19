<template>
  <div class="navbar">
    <router-link to="/" class="title">
      <div id="navbar">Employee Manager</div>
    </router-link>
    <p v-if="isLoggedIn">{{currentUser}}</p>
    <ul>
      <li v-if="isLoggedIn">
        <router-link to="/">Dashborad</router-link>
      </li>
      <li v-if="!isLoggedIn">
        <router-link to="/login">Login</router-link>
      </li>
      <li v-if="!isLoggedIn">
        <router-link to="/register">Register</router-link>
      </li>
      <li v-if="isLoggedIn">
        <button @click="logout">Logout</button>
      </li>
    </ul>
  </div>
</template>

<script>
import firebase from "firebase";

export default {
  name: "navbar",
  data() {
    return {
      isLoggedIn: false,
      currentUser: false
    };
  },
  created() {
    if (firebase.auth().currentUser) {
      this.isLoggedIn = true;
      this.currentUser = firebase.auth().currentUser.email;
    }
  },
  methods: {
    logout() {
      firebase
        .auth()
        .signOut()
        .then(() => {
          // this.$router.push("/login");
          this.$router.go({ path: this.$router.path });
        });
    }
  }
};
</script>

<style scoped>
.navbar {
  background-color: cadetblue;
  padding: 10px;
  display: flex;
  align-items: center;
}
.title {
  flex-grow: 1;
  color: white;
}
li {
  display: inline-block;
  padding: 5px;
  border: black 1px solid;
  border-radius: 5px;
  margin: 3px;
}
</style>