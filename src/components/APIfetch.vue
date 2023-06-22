<template>
  <h1>Maakeetoo API Fetch</h1>
  <div>
    <h3>Form Responses</h3>
    <table class="table">
      <thead class="thead-dark">
        <tr>
          <th scope="col">ID</th>
          <th scope="col">First Name</th>
          <th scope="col">Email</th>
          <th scope="col">Message</th>
          <th scope="col">Form ID</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="response in APIData" :key="response.id">
          <td scope="row">{{ response.id }}</td>
          <td scope="row">{{ response.firstname }}</td>
          <td scope="row">{{ response.email }}</td>
          <td scope="row">{{ response.message }}</td>
          <td scope="row">{{ response.form }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  data() {
    return {
      APIData: [],
    };
  },
  mounted() {
    var axios = require("axios");
    axios
      .get("https://forms.maakeetoo.com/formapi/159", {
        headers: {
          Code: "8UREARVPHWUWQHI0QOFD9WXED",
        },
      })
      .then((response) => {
        this.APIData = response.data;
        console.log(JSON.stringify(response.data));
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>
<style scoped>
.table{
    width: 70vw;
    position: relative;
    left: 50%;
    transform: translate(-50%);
}
</style>