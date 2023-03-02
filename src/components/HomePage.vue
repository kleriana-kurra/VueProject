<template>
  <h1>Welcome to our community💜!</h1>
</template>

<script>
export default {
  name: 'HomePage',
  mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
  },
};
</script>
