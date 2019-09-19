<template>
  <div>
    <h3>Register</h3>
    <form>
      <div class="inputContainer">
        <label>Email</label>
        <input type="text" required class="inputField" v-model="email" />
      </div>
      <div class="inputContainer">
        <label>Password</label>
        <input type="password" required class="inputField" autocomplete="false" v-model="password" />
      </div>
      <input
        type="submit"
        value="register"
        class="inputField"
        autocomplete="false"
        @click="register"
      />
    </form>
  </div>
</template>

<script>
import firebase from "firebase";

export default {
  name: "register",
  data() {
    return {
      email: "",
      password: ""
    };
  },
  methods: {
    register(e) {
      e.preventDefault();
      firebase
        .auth()
        .createUserWithEmailAndPassword(this.email, this.password)
        .then(
          user => {
            alert(`Account created for ${user.user.email}`);
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