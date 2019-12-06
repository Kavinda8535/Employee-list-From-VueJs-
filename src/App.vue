<template>
  <div id="app">
    <h1>Employees & New Commers</h1>

    <!-- <employee-form :employeeform="employeeforms"/> -->
    <employee-form @add:employee="addEmployee" />
    <employee-table 
    :employees="employees" 
    @delete:employee="deleteEmployee"
    @edit:employee="editEmployee"/>
    <newcomer-table :newcomers="newcomers"/>

    <!-- this is the same thing -->
<!-- <employee-table v-bind:employees="employees" /> -->
  </div>
</template>

<script>
import EmployeeTable  from './components/EmployeeTable.vue'
import NewcomerTable  from './components/NewComerTable.vue'
import EmployeeForm   from './components/EmployeeForm.vue'

export default {
  name: 'app',
  components: {
    EmployeeForm,
    EmployeeTable,
    NewcomerTable,
  },
  data()
  {
    return{
      employees:[
        {
          id: 1,
          name: "Saman Kumara",
          email: "Saman@idp.com",
        },
        {
          id: 2,
          name: 'Bertrum Nihal',
          email: 'Burtrum@cinama.io',
        },
        {
          id: 3,
          name: 'Dinesh Colabage',
          email: 'Senid@my.net',
        },
      ],

      newcomers:[
        {
          id: 1,
          name: "Saman Kumara New",
          email: "SamanNew@idp.com",
        },
        {
          id: 2,
          name: 'Bertrum Nihal New',
          email: 'BurtrumNew@cinama.io',
        },
        {
          id: 3,
          name: 'Dinesh Colabage New',
          email: 'SenidNew@my.net',
        },
      ],

    }
  },

  methods:{
    addEmployee(employee){
      this.employees = [...this.employees, employee]
    },
    deleteEmployee(id){
      this.employees = this.employees.filter(
        employee => employee.id !== id
      )
    },
    editEmployee(id, updateEmployee){
      this.employee = this.employee.map(employee =>
      employee.id === id ? updateEmployee : employee
      )
    }

  }

}
</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }

  button:hover,
  button:active,

  button:focus {
  background: #32a95d;
  border: 1px solid #32a95d;
  }

  .small-container {
    max-width: 680px;
  }
</style>
