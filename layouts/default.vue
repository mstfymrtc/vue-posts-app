<template>
  <v-app dark>
    <v-toolbar :clipped-left="clipped" fixed app>
      <v-toolbar-title v-text="title" />
      <v-spacer />
      <v-btn v-if="isInProtectedRoute()" icon @click="logOut">
        <v-icon>logout</v-icon>
      </v-btn>
    </v-toolbar>
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'apps',
          title: 'Welcome',
          to: '/'
        }
      ],
      miniVariant: false,
      right: false,
      rightDrawer: false,
      title: 'Posts App'
    }
  },

  methods: {
    logOut() {
      sessionStorage.removeItem('token')
      this.$router.push('/login')
      this.isLoggedIn = false
    },
    isInProtectedRoute() {
      //auth middleware kullanmak gerekiyor, temp çözüm!
      return this.$route.path == '/app' ? true : false
    }
  }
}
</script>
