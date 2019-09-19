<template>
  <div id="view-employee">
    <h3>View Employee</h3>
    <h4>{{name}}</h4>
    <ul>
      <li>Employee ID: {{employee_id}}</li>
      <li>Department: {{dept}}</li>
      <li>Position: {{position}}</li>
    </ul>
    <router-link to="/">Back</router-link>
    <button @click="deleteEmployee">Delete</button>
    <router-link :to="{name: 'edit-employee', params: {employee_id: employee_id}}">Edit</router-link>
  </div>
</template>

<script>
import db from "./firebaseInit";

export default {
  name: "view-employee",
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
    deleteEmployee() {
      if (confirm("are you sure?")) {
        db.collection("employees")
          .where("employee_id", "==", this.$route.params.employee_id)
          .get()
          .then(snapshot =>
            snapshot.forEach(doc => {
              doc.ref.delete();
              this.$router.push("/");
            })
          );
      }
    }
  }
};
</script>