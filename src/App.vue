<template>
  <div id="app">
    <input type="password" id="password" placeholder="Enter password" />
    <button onclick="checkPassword()">Submit</button>
    <div id="content" style="display: none">
      <el-menu
        :default-active="$router.currentRoute.path"
        mode="horizontal"
        :router="true"
      >
        <el-menu-item index="/">Interview Copilot</el-menu-item>
        <el-menu-item index="/setting">Setting</el-menu-item>
      </el-menu>
      <router-view class="router_view" />
    </div>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
<script>
import { mapGetters } from "vuex";

export default {
  name: "App",
  props: {},
  computed: {},
  beforeMount() {},
  mounted() {},
  data() {
    return {
      activeIndex: "/",
    };
  },
  methods: {},
};
function checkPassword() {
  var password = document.getElementById("password").value;
  if (sha256(password) === "1a9512b68107e4e2f2eb0acb60b50e7bb0a41dd0") {
    document.getElementById("login-form").style.display = "none";
    document.getElementById("content").style.display = "block";
  } else {
    alert("Incorrect password");
  }
}

function sha256(plain) {
  const crypto = window.crypto || window.msCrypto;
  const encoder = new TextEncoder();
  const data = encoder.encode(plain);
  return crypto.subtle.digest("SHA-256", data).then((hash) => {
    return Array.from(new Uint8Array(hash))
      .map((byte) => {
        return ("0" + (byte & 0xff).toString(16)).slice(-2);
      })
      .join("");
  });
}
</script>
<style>
.router_view {
  margin-top: 10px;
}
</style>
