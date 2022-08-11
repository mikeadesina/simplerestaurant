<template>
  <Header />
  <h2>Welcome to Add Page</h2>
  <form class="add">
    <input type="text" v-model="restaurant.name" placeholder="Enter Name" />
    <input
      type="text"
      v-model="restaurant.address"
      placeholder="Enter Address"
    />
    <input
      type="text"
      v-model="restaurant.contact"
      placeholder="Enter Contact"
    />
    <button type="button" v-on:click="addRestaurant">Add New</button>
  </form>
</template>

<script>
import Header from "./Header.vue";
import axios from "axios";
export default {
  name: "Add",
  components: {
    Header,
  },
  data() {
    return {
      restaurant: {
        name: "",
        address: "",
        contact: "",
      },
    };
  },
  methods: {
    async addRestaurant() {
      let result = await axios.post("http://localhost:3000/restaurant", {
        name: this.restaurant.name,
        address: this.restaurant.address,
        contact: this.restaurant.contact
      });
      if (result.status == 201) {
        console.log(result);
        //alert('successful')
        //localStorage.setItem('user-info',JSON.stringify(result.data))
        this.$router.push({ name: "Home" });
      } else {
        alert("not successful");
        console.log(result);
      }
    },
  },
  mounted() {
    let users = localStorage.getItem("user-info");
    if (!users) {
      this.$router.push({ name: "SignUp" });
    }
  },
};
</script>

<style scoped>
.add input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-bottom: 30px;
  margin-right: auto;
  margin-left: auto;
  border: 1px solid skyblue;
}
.add button {
  width: 300px;
  height: 40px;
  border: 1px solid skyblue;
  background: skyblue;
  color: #fff;
  cursor: pointer;
}
</style>
