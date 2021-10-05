<template>
  <div id="app2">
    <nav>
      <div>
        <router-link to="/">
          Home
        </router-link>
        <router-link to="/login" v-if="!authenticated">
          Login
        </router-link>
        <router-link to="/profile" v-if="authenticated" >
          Profile
        </router-link>
        <a v-if="authenticated" v-on:click="logout()">
          Logout
        </a>
      </div>
    </nav>
    <div id="content">
      <router-view/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data: function () {
    return { authenticated: false }
  },
  async created () {
    await this.isAuthenticated()
    this.$auth.authStateManager.subscribe(this.isAuthenticated)
  },
  watch: {
    // Everytime the route changes, check for auth status
    '$route': 'isAuthenticated'
  },
  methods: {
    async isAuthenticated () {
      this.authenticated = await this.$auth.isAuthenticated()
    },
    async logout () {
      await this.$auth.signOut()
    }
  }
}
</script>

<style>
nav div a { margin-right: 10px }
#app {
  width: 800px;
  margin: 0 auto;
}
a {
  text-decoration: underline;
  cursor: pointer;
}
</style>