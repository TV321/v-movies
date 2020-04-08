<template>
    <div>
        <Header title="MOVIE DETAILS"/>
        <MovieDetailsCard />
        <h3>{{ movieId }}</h3>
    </div>
</template>

<script>
import MovieDetailsCard from '@/components/MovieDetailsCard.vue'
import Header from '@/components/Header.vue'


export default {
  name: 'MovieDetails',
  props: ['movieId'],
  components: {
    MovieDetailsCard,
    Header

  }
}
</script>