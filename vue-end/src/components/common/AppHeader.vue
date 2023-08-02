<template>
  <div>
    <router-link to="/"> TIL </router-link>
    <header>
      <template v-if="isUserLogin">
        <span>{{ $store.state.username }}</span>
        <a href="javascript:''" @click="logOutUser">로그아웃</a>
      </template>
      <template v-else>
        <router-link to="login">로그인</router-link> |
        <router-link to="signup"> 회원가입</router-link>
      </template>
    </header>
  </div>
</template>

<script>
export default {
  computed: {
    isUserLogin() {
      return this.$store.getters.isLogin;
    },
  },
  methods: {
    logOutUser() {
      this.$store.commit('clearUsername');
      this.$router.push('/login');
    },
  },
};
</script>
