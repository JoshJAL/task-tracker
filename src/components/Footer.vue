<template>
  <footer>
    <p>Copyright &copy; 2022</p>
    <router-link :to="aboutPage ? '/' : '/about'">{{ aboutPage ? 'Go Home' : "About" }}</router-link>
  </footer>
</template>

<style scoped>
  a {
    color: #333;
  }

  footer {
    margin: 30px 0 0 0;
    text-align: center;
  }
</style>

<script>
  export default {
    name: "Footer",
    computed: {
      aboutPage() {
        if (this.$route.path === '/about') {
          return true;
        } else {
          return false;
        }
      }
    }
  }
</script>