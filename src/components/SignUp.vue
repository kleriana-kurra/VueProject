<template>
  <img class="logo" src="../assets/logo.jpg" />
  <h1>SignUp</h1>
  <div class="register">
    <input type="text" v-model="name" placeholder="Enter Name" />
    <input type="text" v-model="email" placeholder="Enter Email" />
    <input type="text" v-model="password" placeholder="Enter Password" />
    <button @click="signUp">Sign Up</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "SignUp",
  data() {
    return {
      name: "",
      email: "",
      password: "",
    };
  },
  methods: {
    async signUp() {
      let result = await axios.post("http://localhost:3000/users", {
        email: this.email,
        password: this.password,
        name: this.name,
      });
      console.warn(result);
      if (result.status == 201) {
        localStorage.setItem("user-info", JSON.stringify(result.data));
        this.$router.push({ name: "HomePage" });
      }
    },
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (user) {
      this.$router.push({ name: "HomePage" });
    }
  },
};
</script>

<style scoped>
.logo {
  width: 150px;
  height: 150px;
}

.register {
  display: grid;
  justify-content: center;
}

.register input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;

  margin-bottom: 30px;
  margin-right: auto;
  border: 1px solid #1ca8ff;
}
.register button {
  width: 320px;
  height: 40px;
  border: 2px solid #ffd500;
  background-color: #ffd500;
  color: #2c3e50;
  font-weight: 600;
  cursor: pointer;
}
</style>
