<template>
  <div id="dashboard">
    <h3>Dashboard</h3>
    <h4>Employees</h4>
    <ul>
      <li v-for="employee in employees" :key="employee.id">
        <div class="dept">{{employee.dept}}</div>
        <div class="names">{{employee.employee_id}}:{{employee.name}}</div>
        <div class="dept">
          <router-link
            :to="{name: 'view-employee', params: {employee_id: employee.employee_id}}"
          >View</router-link>
        </div>
      </li>
    </ul>
    <div class="newEmployeeBtnContainer">
      <router-link class="newEmployeeBtn" to="/new">Add+</router-link>
    </div>
  </div>
</template>

<script>
import db from "./firebaseInit";

export default {
  name: "dashboard",
  data() {
    return {
      employees: []
    };
  },
  created() {
    db.collection("employees")
      .orderBy("dept")
      .get()
      .then(snapshot => {
        snapshot.forEach(doc => {
          const data = {
            id: doc.id,
            employee_id: doc.data().employee_id,
            name: doc.data().name,
            dept: doc.data().dept,
            position: doc.data().position
          };
          this.employees.push(data);
        });
      });
  }
};
</script>

<style scoped>
h4 {
  margin-top: 30px;
}
li {
  padding: 20px;
  border: 1px rgb(172, 172, 172) solid;
  display: flex;
  justify-content: space-between;
}
.dept {
  display: inline-block;
  width: 50px;
  background-color: grey;
  border-radius: 5px;
  text-align: center;
  color: white;
  margin-right: 10px;
}
.names {
  flex-grow: 1;
}
.newEmployeeBtnContainer {
  margin-top: 30px;
}
.newEmployeeBtn {
  background-color: crimson;
  border-radius: 10px;
  padding: 4px;
  color: white;
}
</style>