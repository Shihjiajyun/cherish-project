<template>
  <Navbar></Navbar>
  <div class="container-fluid"><router-view/></div>
</template>

<script>
import Navbar from '../components/NavbarView.vue';

export default {
  components: {
    Navbar,
  },
  created() {
    const token = document.cookie.replace(/(?:(?:^|.*;\s*)cherishToken\s*=\s*([^;]*).*$)|^.*$/, '$1');
    // console.log(token);
    this.$http.defaults.headers.common.Authorization = token;
    const api = `${process.env.VUE_APP_API}api/user/check`;
    this.$http.post(api, this.user)
      .then((res) => {
        console.log(res);
        if (!res.data.success) {
          this.$router.push('login');
        }
      });
  },
};
</script>
