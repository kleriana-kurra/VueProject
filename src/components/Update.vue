<template>
  <Header/>
  <h1>Hello User, Welcome to update Page</h1>
</template>

<script>
import Header from "@/components/Header.vue";
export default {
  name: 'UpdatePage',
  components: { Header },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
  },
};
</script>
