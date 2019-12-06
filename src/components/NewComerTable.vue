<template>

  <div id="newcomer-table">
    <table>
      <thead>
        <tr>
          <th>Newcommer name</th>
          <th>Newcommer email</th>
        </tr>
      </thead>
      <tbody>

        <tr v-for="newcomer in newcomers" :key="newcomer.id">
            <td>{{ newcomer.name}}</td>
            <td>{{ newcomer.email}}</td>
        </tr>

      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'newcomer-table',
  props: {
      newcomers: Array,
  }

  
}
</script>

<style scoped></style>
