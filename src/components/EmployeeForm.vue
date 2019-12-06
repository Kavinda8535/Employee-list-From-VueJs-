<template> 
  <div id="employee-form">
    <form @submit.prevent="handleSubmit">

    <!-- </form> -->
    <!-- <form> -->
      <label>Employee name</label>

      <input
        ref="first"
        type="text"
        :class="{ 'has-error': submitting && invalidName }"
        v-model="employee.name"
        @focus="clearStatus"
        @keypress="clearStatus"
        />
        <p>{{ charactorCounter }}/100</p>
      
      <label>Employee Email</label>
        <input
        type="text"
        :class="{ 'has-error': submitting && invalidEmail }"
        v-model="employee.email"
        @focus="clearStatus"
        />
        <p>{{ charactorCounter }}/100</p>
        <p v-if="includeAtSign">Its a correct mail address.</p>

      <p v-if="error && submitting" class="error-message">
        ❗Please fill out all required fields
      </p>
      <p v-if="success" class="success-message">
         ✅ Employee successfully added
      </p>

      <button>Add Employee</button>
    </form>
  </div>
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
      //console.log('testing')
      //alert('Testing handleSubmit method')
      this.submitting = true;
      this.clearStatus();

      if (this.invalidName || this.invalidEmail) {
        this.error = true;
        return;
      }
      this.$emit("add:employee", this.employee);
      this.$refs.first.focus();// Focus for the first text box
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
    },

    addEmployee(employee) {
      const lastId =
        this.employees.length > 0
          ? this.employees[this.employees.length - 1].id
          : 0;
      const id = lastId + 1;
      const newEmployee = { ...employee, id };
      this.employees = [...this.employees, newEmployee];
    }
  },

  computed: {
    //Change the presentation of existig data we use computed functions. 
    //But if you need to change data you should use methods. (Methods vs computed)
    invalidName() {
      return this.employee.name === "";
    },

    invalidEmail() {
      return this.employee.email === "";
    },

    //counting the charactors in the text field
    charactorCounter() {
      return this.employee.name.length;
    },

    //checking specific charactors are in the text field
    includeAtSign() {
      return this.employee.email.includes('@');
    }
  }
};
</script>

<style scoped>
form {
  margin-bottom: 2rem;
}

[class*="-message"] {
  font-weight: 500;
}

.error-message {
  color: #d33c40;
}

.succuess-message {
  color: #32a95d;
}
</style>
