<template>
    <div>
        <Header title="MOVIE DETAILS"/>
        <MovieDetailsCard :guestId="guestId"/>
    </div>
</template>

<script>
import MovieDetailsCard from '@/components/MovieDetailsCard.vue'
import Header from '@/components/Header.vue'


export default {
  name: 'MovieDetails',
  props: ['movieId', 'guestId'],
  components: {
    MovieDetailsCard,
    Header

  }
}
</script>