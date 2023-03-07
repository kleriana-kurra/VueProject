<template>
  <Header />
  <h1>Hello User, Welcome to update Page</h1>
  <form class="add">
    <input
      type="text"
      name="name"
      placeholder="Enter Name"
      v-model="restaurant.name"
    />
    <input
      type="text"
      name="address"
      placeholder="Enter Address"
      v-model="restaurant.address"
    />
    <input
      type="text"
      name="contact"
      placeholder="Enter Contact"
      v-model="restaurant.contact"
    />
    <button type="button" v-on:click="updateRestaurant">Add new restaurant</button>
  </form>
</template>

<script>
import Header from "@/components/Header.vue";
import axios from "axios";
export default {
  name: "UpdatePage",
  components: { Header },
  data() {
    return {
      restaurant: {
        name: "",
        address: "",
        contact: "",
      },
    };
  },
  methods:{
    async updateRestaurant(){
      console.warn(this.restaurant)
      console.warn(this.restaurant);
      const result = await axios.put('http://localhost:3000/restaurants/' + this.$route.params.id, {
        name: this.restaurant.name,
        address: this.restaurant.address,
        contact: this.restaurant.contact,
      });
      if(result.status == 200)
      {
        this.$router.push({ name: "HomePage" });
      }
    }
  },
  async mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
    const result = await axios.get(
      'http://localhost:3000/restaurants/' + this.$route.params.id
    );
    // console.warn(this.$route.params.id);
    console.warn(result.data);
    this.restaurant = result.data;
  },
};
</script>

<style scoped>
.add {
  display: grid;
  justify-content: center;
}

.add input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;

  margin-bottom: 30px;
  margin-right: auto;
  border: 1px solid #1ca8ff;
}

.add button {
  width: 320px;
  height: 40px;
  border: 2px solid #ffd500;
  background-color: #ffd500;
  color: #2c3e50;
  font-weight: 600;
  cursor: pointer;
}
</style>
