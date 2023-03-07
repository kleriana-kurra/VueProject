<template>
  <Header/>
  <h1>Welcome to our community {{name}}💜!</h1>
  <table border="1">
    <tr>
      <td>Id</td>
      <td>Name</td>
      <td>Contact</td>
      <td>Address</td>
    </tr>
    <tr v-for="item in restaurants" :key="item.id">
      <td>{{item.id}}</td>
      <td>{{item.name}}</td>
      <td>{{item.contact}}</td>
      <td>{{item.address}}</td>
    </tr>
  </table>
</template>

<script>
import axios from "axios";
import Header from "@/components/Header.vue";
export default {
  name: "HomePage",
  data(){
    return{
      name: '',
      restaurants: [],
    }
  },
  components: { Header },
  async mounted() {
    let user = localStorage.getItem("user-info");
    this.name = JSON.parse(user).name;
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
    let result = await axios.get("http://localhost:3000/restaurants");
    console.warn(result);
    this.restaurants = result.data;
  },
};
</script>


<style scoped>

td{
  width: 160px;
  height: 40px;
}

</style>
