<template>
  <div class="container">
    <q-markup-table>
      <thead>
        <tr>
          <th class="text-left">ID</th>
          <th class="text-right">Name</th>
          <th class="text-right">Email</th>
          <th class="text-right">Phone</th>
          <th class="text-right">Password</th>
          <th class="text-right">Edit</th>
          <th class="text-right">Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in allData" :key="user.id">
          <td class="text-left">{{ user.acc_id }}</td>
          <td class="text-right">{{user.acc_name}}</td>
          <td class="text-right">{{user.acc_email}}</td>
          <td class="text-right">{{user.acc_phone}}</td>
          <td class="text-right">{{user.acc_password}}</td>
          <td class="text-right">
            <q-btn color="deep-purple-8" label="Edit" />
          </td>
          <td class="text-right">
            <q-btn color="red-10" label="Delete" @click="deleteData(user.acc_id)" />
          </td>
        </tr>
      </tbody>
    </q-markup-table>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "DashBord",
  data() {
    return {
      allData: "",
      url_api_plan: "http://localhost/my_account/api_account.php"
    };
  },
  methods: {
    deleteData(id) {
      let c = confirm("Are you sure to delete ?.");
      if (c == true) {
        axios
          .post(this.url_api_plan, {
            action: "delete",
            // ลบ id ที่รับมา
            acc_id: id
          })
          .then(res => {
            console.log("delete", res.data);
          })
          .catch(function(error) {
            console.log(error);
          });
      }
      this.getData();
    },
    getData() {
      axios
        .post(this.url_api_plan, {
          action: "select"
        })
        .then(res => {
          //   console.log(res.data);
          this.allData = res.data;
          //   console.log(this.allData[1].acc_id);
        });
    }
  },
  created() {
    this.getData();
  }
};
</script>

<style>
</style>