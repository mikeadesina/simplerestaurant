<template>
  <Header />
  <h2>Welcome {{ name }} to My Restaurant Page</h2>
  <table border="1">
    <tr>
      <td>Id</td>
      <td>Name</td>
      <td>Contact</td>
      <td>Address</td>
      <td>Action</td>
    </tr>
    <tr v-for="item in restaurant" :key="item.id">
      <td>{{ item.id }}</td>
      <td>{{ item.name }}</td>
      <td>{{ item.contact }}</td>
      <td>{{ item.address }}</td>
      <td>
        <router-link :to="'/update/' + item.id">update</router-link
        > <button type="button" v-on:click="deleteRestaurant(item.id)">
          Delete
        </button>
      </td>
    </tr>
  </table>
</template>

<script>
import Header from "./Header.vue";
import axios from "axios";
export default {
  name: "Home",
  data() {
    return {
      name: "",
      restaurant: [],
    };
  },
  components: {
    Header,
  },
  methods: {
    async deleteRestaurant(id) {
        alert(id);
        const deleteRecord = await axios.delete(
        `http://localhost:3000/restaurant/${id}`
      );
      console.log(deleteRecord);
      if ((result.status == 200)) {
        this.loadData();
      }
    //   const result = await axios.delete(
    //     `http://localhost:3000/restaurant?id=${id}`
    //   );
    
    },
    async loadData() {
      let users = localStorage.getItem("user-info");
      this.name = JSON.parse(users).name;
      if (!users) {
        this.$router.push({ name: "SignUp" });
      }
      let result = await axios.get(`http://localhost:3000/restaurant`);
      this.restaurant = result.data;
      console.log(result);
    },
  },
  async mounted() {
    this.loadData();
  },
};
</script>

<style>
td {
  width: 160px;
  height: 40px;
}
</style>
