
<template>
  <v-toolbar fixed dark class="teal accent-4" >
    <v-toolbar-title class="mr-4 home" @click="navigateTo({name: 'root'})">
      TabTracker
    </v-toolbar-title>

    <v-toolbar-items>
      <v-btn
       flat dark @click="navigateTo({name: 'songs'})">
        Browse
      </v-btn>
    </v-toolbar-items>
    <v-spacer></v-spacer>
    <v-toolbar-items>
      <v-btn
      v-if="!$store.state.isUserLoggedIn"
      flat dark @click="navigateTo({name: 'login'})">
        Login
      </v-btn>
      <v-btn
      v-if="$store.state.isUserLoggedIn"
      flat dark @click="logout">
        Log Out
      </v-btn>
      <v-btn
      v-if="!$store.state.isUserLoggedIn"
       flat dark @click="navigateTo({name: 'register'})">
        Sign Up
      </v-btn>
    </v-toolbar-items>
  </v-toolbar>
</template>

<script>
/* eslint-disable */

export default {
methods: {
  navigateTo: function(route){
    this.$router.push(route);
  },
  logout: function () {
    this.$store.dispatch('setToken', null)
    this.$store.dispatch('setUser', null)
    // TODO: redirect to homepage
    this.$router.push({name: 'root'})
  }
}
}
</script>
<style scoped>
.home{
  cursor: pointer;
}
</style>
