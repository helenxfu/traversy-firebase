<template>
  <div id="edit-employee">
    <h3>Edit Employee</h3>
    <div>
      <form @submit.prevent="updateEmployee">
        <div class="row">
          <label>Employee ID#</label>
          <input type="text" v-model="employee_id" disabled />
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
  name: "edit-employee",
  data() {
    return {
      employee_id: null,
      name: null,
      dept: null,
      position: null
    };
  },
  beforeRouteEnter(to, from, next) {
    db.collection("employees")
      .where("employee_id", "==", to.params.employee_id)
      .get()
      .then(snapshot => {
        snapshot.forEach(doc => {
          next(vm => {
            vm.employee_id = doc.data().employee_id;
            vm.name = doc.data().name;
            vm.dept = doc.data().dept;
            vm.position = doc.data().position;
          });
        });
      });
  },
  watch: {
    $route: "fetchData"
  },
  methods: {
    fetchData() {
      db.collection("employees")
        .where("employee_id", "==", this.$route.params.employee_id)
        .get()
        .then(snapshot =>
          snapshot.forEach(doc => {
            this.employee_id = doc.data().employee_id;
            this.name = doc.data().name;
            this.dept = doc.data().dept;
            this.position = doc.data().position;
          })
        );
    },
    updateEmployee() {
      db.collection("employees")
        .where("employee_id", "==", this.$route.params.employee_id)
        .get()
        .then(snapshot =>
          snapshot.forEach(doc => {
            doc.ref
              .update({
                employee_id: this.employee_id,
                name: this.name,
                dept: this.dept,
                position: this.position
              })
              .then(() => {
                this.$router.push({
                  name: "view-employee",
                  params: { employee_id: this.employee_id }
                });
              });
          })
        );
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