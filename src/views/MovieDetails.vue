<template>
    <div>
        <Header title="MOVIE DETAILS"/>
        <MovieDetailsCard :guestId="guestId"/>
        <h3>{{ movieId }}</h3>
        <h3>{{ testData }}</h3>
    </div>
</template>

<script>
import MovieDetailsCard from '@/components/MovieDetailsCard.vue'
import Header from '@/components/Header.vue'


export default {
  name: 'MovieDetails',
  props: ['movieId', 'testData', 'guestId'],
  components: {
    MovieDetailsCard,
    Header

  }
}
</script>