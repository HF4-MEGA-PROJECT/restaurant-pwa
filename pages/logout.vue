<template>
  <div></div>
</template>

<script>
export default {
  data() {
    return {}
  },

  computed: {
    user() {
      return this.$store.state.user
    }
  },

  created() {
    this.logout();
  },

  methods: {
    logout() {
      if (this.user === null) {
        this.$router.push('/');
        return;
      }

      this.$auth.logout();
    },
  },
}
</script>
