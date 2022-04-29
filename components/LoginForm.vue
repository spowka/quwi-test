<template>
  <div class="loginFormContainer">
    <div class="loginForm">
      <div class="logo">
        <img src="~assets/quwi-logo.png" width="40" height="40" alt="" />
        <p style="font-size: 24px">QUWI</p>
      </div>
      <div class="input">
        <input type="email" placeholder="email" v-model="email" />
      </div>
      <div class="input">
        <input type="password" placeholder="password" v-model="password" />
      </div>
      <button class="button" @click="login">Login</button>
      <button class="forgot">Forgot password?</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "LoginForm",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    login() {
      this.$axios
        .$post("/auth/login", {
          email: this.email,
          password: this.password,
        })
        .then((res) => {
          console.log(res);
          localStorage.setItem("access_token", res.token);
          this.email = "";
          this.password = "";
          this.$router.push("/home");
        });
    },
  },
};
</script>

<style scoped>
.loginFormContainer {
  background-image: url("~assets/gray_blur.png");
  height: calc(100vh - 45px);
  display: flex;
  justify-content: center;
  align-items: center;
}
.loginForm {
  width: 440px;
  height: 353px;
  padding: 25px 40px 35px;
  background: #fff;
  text-align: center;
  box-shadow: 0 0 12px rgb(0 0 0 / 25%);
  border-radius: 15px;
}
.logo {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 14px;
  margin-bottom: 40px;
}
.input {
  width: 100%;
}
.input input {
  width: 100%;
  height: 48px;
  padding: 15px;
  outline: none;
  border: 1px solid #dadada;
  border-radius: 5px;
  margin-bottom: 15px;
}
.button {
  width: 100%;
  height: 48px;
  border: none;
  border-radius: 5px;
  background: #2668c1;
  color: #fff;
  font-size: 18px;
  margin: 10px 0 15px;
  cursor: pointer;
}
.forgot {
  background: none;
  border: none;
  color: #2668c1;
  padding: 0;
}
</style>
