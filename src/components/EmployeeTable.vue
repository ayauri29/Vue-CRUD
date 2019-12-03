<template lang="pug">
  div#employee-table
    p(v-if="employees.length < 1") No employees
    table(v-else)
      thead
        tr
          th Employee name
          th Employee email
          th Actions
      tbody
        tr(v-for="employee in employees" :key="employee.id")
          td(v-if="editing === employee.id")
            input(type="text" v-model="employee.name")
          td(v-else) {{ employee.name}}
          td(v-if="editing === employee.id")
            input(type="text" v-model="employee.email")
          td(v-else) {{ employee.email}}
          td(v-if="editing === employee.id")
            button(@click="editEmployee(employee)") Save
            button(class="muted-button" @click="editing = null") Cancel
          td(v-else class="td-actions")
            button(@click="editMode(employee.id)") Edit
            button(@click="$emit('delete:employee', employee.id)") Delete
</template>

<script>
export default {
  name: "employee-table",
  props: {
    employees: Array
  },
  data() {
    return {
      editing: null
    };
  },
  methods: {
    editMode(id) {
      this.editing = id;
    },

    editEmployee(employee) {
      if (employee.name === "" || employee.email === "") return;
      this.$emit("edit:employee", employee.id, employee);
      this.editing = null;
    }
  }
};
</script>

<style scoped lang="stylus" scoped>
.td-actions
  display flex
  justify-content space-around
button 
 color white
 background-color #3e51d8
 border 1px solid #3e51d8
 font-size 12px
</style>
