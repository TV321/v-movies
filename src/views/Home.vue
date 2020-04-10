<template>
  <div class="home">
    <Header title="MOVIES" :display="display" :onChange="onInputChange"/>
    <CardsContainer :display="display"/>
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
  },
  data() {
    return {
      display: "popular"
    }
  },
  methods: {
    onInputChange(valueOfInput) {
      this.display = valueOfInput
    }
  }
}
</script>
