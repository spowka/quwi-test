<template>
  <div class="header">
    <img src="~assets/quwi-logo.png" width="20" height="20" alt="" />
    <div v-if="$nuxt.$route.path === '/'"><p>SignUp</p></div>
    <div v-else>
      <p>Projects</p>
      <p @click="logOute">LOGOUT</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Header",
  methods: {
    logOute() {
      this.$axios({
        url: "/auth/logout",
        method: "post",
        headers: {
          Authorization: `Bearer ${localStorage.getItem("access_token")}`,
        },
      }).then(() => {
        localStorage.clear();
        this.$router.push("/");
      });
    },
  },
};
</script>

<style scoped>
.header {
  position: relative;
  z-index: 10;
  display: flex;
  height: 45px;
  justify-content: space-between;
  align-items: center;
  padding: 0 33px;
  box-shadow: 0px 5px 13px -8px rgba(34, 60, 80, 0.6);
  text-transform: uppercase;
}
.header div {
  display: flex;
  gap: 20px;
  font-size: 12px;
}
p {
  cursor: pointer;
}
</style>
>
