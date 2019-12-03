<template lang="pug">
  div#app.small-container
    div#form.form-container
      h1.title Employees
      employee-form(@add:employee="addEmployee")
    div#table.table-container
      employee-table(
        :employees="employees"
        @delete:employee="deleteEmployee"
        @edit:employee="editEmployee")
</template>

<script>
import EmployeeTable from "./components/EmployeeTable.vue";
import EmployeeForm from "@/components/EmployeeForm.vue";

export default {
  name: "app",
  components: {
    EmployeeTable,
    EmployeeForm
  },
  data() {
    return {
      employees: [
        {
          id: 1,
          name: "Richard Hendricks",
          email: "richard@piedpiper.com"
        },
        {
          id: 2,
          name: "Bertram Gilfoyle",
          email: "gilfoyle@piedpiper.com"
        },
        {
          id: 3,
          name: "Dinesh Chugtai",
          email: "dinesh@piedpiper.com"
        }
      ]
    };
  },
  methods: {
    addEmployee(employee) {
      const lastId =
        this.employees.length > 0
          ? this.employees[this.employees.length - 1].id
          : 0;
      const id = lastId + 1;
      const newEmployee = { ...employee, id };

      this.employees = [...this.employees, newEmployee];
    },
    deleteEmployee(id) {
      this.employees = this.employees.filter(
        employee => employee.id !== id
      )
    },
    editEmployee(id, updatedEmployee) {
      this.employees = this.employees.map(employee => 
        employee.id === id ? updatedEmployee : employee
      )
    }
  }
};
</script>

<style lang="stylus" scoped>
.small-container
  font-family 'Open Sans', sans-serif;
  .form-container
    display flex
    flex-direction column
    align-items center
    .title
      color red    
</style>
