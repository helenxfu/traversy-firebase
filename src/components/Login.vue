<template>
  <div>
    <h3>Login</h3>
    <form>
      <div class="inputContainer">
        <label>Email</label>
        <input type="text" required class="inputField" v-model="email" />
      </div>
      <div class="inputContainer">
        <label>Password</label>
        <input type="password" required class="inputField" autocomplete="false" v-model="password" />
      </div>
      <input type="submit" value="send" class="inputField" autocomplete="false" @click="login" />
    </form>
  </div>
</template>

<script>
import firebase from "firebase";

export default {
  name: "login",
  data() {
    return {
      email: "",
      password: ""
    };
  },
  methods: {
    login(e) {
      e.preventDefault();
      firebase
        .auth()
        .signInWithEmailAndPassword(this.email, this.password)
        .then(
          user => {
            alert(`Logged in as ${user.user.email}`);
            // this.$router.push("/");
            this.$router.go({ path: this.$router.path });
          },
          err => {
            alert(err.message);
          }
        );
    }
  }
};
</script>

<style scoped>
.inputContainer {
  display: flex;
  flex-direction: column;
}
.inputField {
  border: 1px solid black;
  padding: 5px;
}
</style>