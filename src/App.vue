<template>
<v-app >
<div id="app">
    
    <keep-alive include="Home">
      <router-view/>
    </keep-alive>
    
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link to="/details">Details</router-link>
    </div>
    
  </div>
  </v-app>
</template>

<script>
export default {
  name: 'App',
  data: () => ({
    //
  }),
};
</script>

<style lang="sass" scoped>
  div#app
    height: 100%
  // html, body
  //   // height: 100%
  //   // border: 1px solid blue
</style>
