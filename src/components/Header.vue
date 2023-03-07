<template>
  <div class="navMenu">
    <router-link to="/">Home</router-link>
    <router-link to="/add">Add Restaurant</router-link>
    <a v-on:click="logout" href="#">Logout</a>
  </div>
</template>

<script>
export default{
  name: 'HeaderComponent',
  methods:{
    logout(){
      localStorage.clear();
      this.$router.push({ name: "Login" })
    }
  }
}
</script>

<style scoped>
.navMenu{
  background-color: #1ca8ff;
  overflow: hidden;
}

.navMenu a{
  float: left;
  color: white;
  padding: 14px;
  text-align: center;
  font-size: 17px;
  text-decoration: none;
}

.navMenu a:hover{
  background: lightpink;
  color: #2c3e50;
}

</style>