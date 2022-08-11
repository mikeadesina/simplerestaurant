<template>
  <Header />
  <h2>Welcome to Update Page</h2>
  <form class="update">
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
    <button type="button" v-on:click="addRestaurant">Update</button>
  </form>
</template>

<script>
import Header from "./Header.vue";
import axios from "axios";
export default {
  name: "Update",
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
  async mounted() {
    let users = localStorage.getItem("user-info");
    if (!users) {
      this.$router.push({ name: "SignUp" });
    }
    let result=await axios.get(`http://localhost:3000/restaurant?id=${this.$route.params.id}`);
    console.log(result);
    if(result.status==200 && result.data.length > 0){
        this.restaurant.name=result.data[0].name;
        this.restaurant.address=result.data[0].address;
        this.restaurant.contact=result.data[0].contact;
        
    }else{
        
    }
  },
};
</script>

<style scoped>
.update input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-bottom: 30px;
  margin-right: auto;
  margin-left: auto;
  border: 1px solid skyblue;
}
.update button {
  width: 300px;
  height: 40px;
  border: 1px solid skyblue;
  background: skyblue;
  color: #fff;
  cursor: pointer;
}
</style>
