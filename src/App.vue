<template>
<v-app class="blue">
<div id="app">
    
    <keep-alive include="Home">
      <router-view :guestId="guestSessionId"/>
    </keep-alive>
    
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link to="/details">Details</router-link>
    </div> -->
    
  </div>
  </v-app>
</template>

<script>
import axios from 'axios'
const key = "dbc9fd3cb8c02c485593e9bf8ba731d7";

export default {
  name: 'App',
  data: () => ({
    guestSessionId: ""
  }),
  mounted() {
    axios
      .get(`https://api.themoviedb.org/3/authentication/guest_session/new?api_key=${ key }`)
      .then(resp => {
        console.log(resp.data.guest_session_id)
        this.guestSessionId = resp.data.guest_session_id
      })
  }
};
</script>

<style lang="sass" scoped>
  div#app
    height: 100%
  // html, body
  //   // height: 100%
  //   // border: 1px solid blue
</style>
