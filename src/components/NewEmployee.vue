<template>
  <div id="new-employee">
    <h3>new Employee</h3>
    <div>
      <form @submit.prevent="saveEmployee">
        <div class="row">
          <label>Employee ID#</label>
          <input type="text" v-model="employee_id" required />
        </div>
        <div class="row">
          <label>Name</label>
          <input type="text" v-model="name" required />
        </div>
        <div class="row">
          <label>Department</label>
          <input type="text" v-model="dept" required />
        </div>
        <div class="row">
          <label>Position</label>
          <input type="text" v-model="position" required />
        </div>
        <button type="submit">Submit</button>
        <router-link to="/">Cancel</router-link>
      </form>
    </div>
  </div>
</template>

<script>
import db from "./firebaseInit";

export default {
  name: "new-employee",
  data() {
    return {
      employee_id: null,
      name: null,
      dept: null,
      position: null
    };
  },
  methods: {
    saveEmployee() {
      db.collection("employees")
        .add({
          employee_id: this.employee_id,
          name: this.name,
          dept: this.dept,
          position: this.position
        })
        .then(() => {
          this.$router.push("/");
        })
        // eslint-disable-next-line no-console
        .catch(err => console.log(err));
    }
  }
};
</script>

<style scoped>
input[type="text"] {
  border: 1px solid black;
  padding: 10px;
}
</style>