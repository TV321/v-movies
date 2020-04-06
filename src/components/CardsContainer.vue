<template>
    <div>
        <h3>Containers for movie cards</h3>
        <Card v-for="(movie, index) in movies" :key="index" :movie="movie"/>
    </div>
</template>

<script>
import Card from './Card.vue'
export default {
    data() {
        return {
            movies: ['apple', 'express', 'jungle', 'randomShizzz']
        }
    },
    components: {
        Card
    }
}
</script>