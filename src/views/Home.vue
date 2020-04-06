<template>
  <div class="home">
    <Header />
    <CardsContainer />
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import Header from '@/components/Header.vue'
import CardsContainer from '@/components/CardsContainer.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld,
    Header,
    CardsContainer
  }
}
</script>
