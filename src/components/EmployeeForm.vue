<template lang="pug">
  div#employee-form.form-container
    form(@submit.prevent="handleSubmit")
      label Employee name
      input(
        ref="first"
        type="text"
        v-model="employee.name")
      label Employee Email
      input(
        type="text"
        v-model="employee.email")
      p(v-if="error && submitting" class="error-message") ❗Please fill out all required fields
      p(v-if="success" class="success-message") ✅Employee successfully added
      button.button-add Add Employee
</template>

<script>
export default {
  name: "employee-form",
  data() {
    return {
      submitting: false,
      error: false,
      success: false,
      employee: {
        name: "",
        email: ""
      }
    };
  },
  methods: {
    handleSubmit() {
      this.submitting = true;
      this.clearStatus();

      if (this.invalidName || this.invalidEmail) {
        this.error = true;
        return;
      }

      this.$emit("add:employee", this.employee);

      this.employee = {
        name: "",
        email: ""
      };
      this.error = false;
      this.success = true;
      this.submitting = false;
    },

    clearStatus() {
      this.success = false;
      this.error = false;
    }
  },
  computed: {
    invalidName() {
      return this.employee.name === "";
    },
    invalidEmail() {
      return this.employee.email === "";
    }
  }
}
</script>

<style lang="stylus" scoped>
  .form-container
    margin-bottom 2rem
    display flex
    .button-add
      color white
      background-color #3e51d8
    .error-message 
      color #d33c40;
    .success-message
      color #32a95d
</style>