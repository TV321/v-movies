<template>
    <div id="cardsContainer">
    <v-container>
        <v-row justify="center">
            <v-col v-for="(movie, index) in movies" :key="index">
                <Card   :movie="movie.title" :cardImg="movie.poster_path" :date="movie.release_date" :lang="movie.original_language"
                    :rating="movie.vote_average" :index="index" :movieId="movie.id"
                />
            </v-col>
        </v-row>
        <v-row justify="end">
            <v-col md="4" class="text-md-center">
                <v-btn @click="onFabClick" light fab color="#FFC107">
                    <v-icon>mdi-plus</v-icon>
                </v-btn>
            </v-col>
            <v-col md="4" class="text-md-right">
                <Modal />
            </v-col>
        </v-row>


    </v-container>
 
    </div>

</template>

<script>
import Card from './Card.vue'
import Modal from './Modal.vue'
import axios from 'axios'

const key = "dbc9fd3cb8c02c485593e9bf8ba731d7";

export default {
    props: {
        display: String
    },
    data() {
        return {
            movies: [],
            page: 2,
            clickedIndex: null,
        }
    },
    components: {
        Card,
        Modal
    },
    mounted(){
        axios
            .get(`https://api.themoviedb.org/3/movie/${ this.display }?api_key=${ key }&language=en-US&page=1`)
            .then(resp => {
                console.log(resp.data.results)
                this.movies = resp.data.results
            })
    },
    methods: {
        onFabClick: function() {
            axios
                .get(`https://api.themoviedb.org/3/movie/${ this.display }?api_key=${ key }&language=en-US&page=${ this.page }`)
                .then(resp => {
                    console.log(resp.data.results)
                    this.movies = [...this.movies, ...resp.data.results]
                    this.page++
                })
        }
    },
    watch: {
        display() {
            console.log('Display changed into: ' + this.display)
            axios
                .get(`https://api.themoviedb.org/3/movie/${ this.display }?api_key=${ key }&language=en-US&page=1`)
                .then(resp => {
                    console.log(resp.data.results)
                    this.movies = resp.data.results
                })
        }
    },
}
</script>

<style lang="sass" scoped>
    div.container
        max-width: 1600px
    div.col
        padding: 10px 5px
        flex-grow: 0

    #cardsContainer
        background-color: #333
  
</style>