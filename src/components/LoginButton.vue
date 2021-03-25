<template>
  <a href="https://saasdemo-xendity-gispatial.vercel.app/#/auth/login">
    Log In</a>
</template>

<script>
export default {
  name: "LoginButton",
  methods: {
    login() {
      this.$auth.loginWithRedirect();
    },
  },
};
</script>
