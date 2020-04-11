<template>
    <div id="cardContainer">
    <v-card
        dark
        class="mx-auto"
        max-width="700"
    >

        <v-card-title class="amber--text headline">{{ movieTitle }}</v-card-title>
        <div id="cardImage">
            <v-img
            v-if="url"
            class="white--text align-end"
            height="350px"
            :src="`https://image.tmdb.org/t/p/original${ url }`"
        >
        </v-img>
        <v-img
            v-else
            class="white--text align-end"
            height="350px"
            src="@/assets/movieDetails.jpg"
        >
        </v-img>
        </div>
        
        
        <v-card-actions class="pa-0">
            <v-card-subtitle class="subtitle-1">Release date: {{ movieDate }}</v-card-subtitle>

            <v-spacer></v-spacer>
            <span class="grey--text text--lighten-2 body-2 mr-0">
                ({{ rating }})
            </span>

            <v-rating color="amber" background-color="#666" hover  class="pa-2"
                :half-increments="true" half-icon="mdi-star-half-full" 
                dense length="10" v-model="rating" :readonly="rating > 0" @input="onRatingClick">
            </v-rating>
        </v-card-actions>

        <v-card-text class="text--primary">
            <div class="white--text body-1"><span class="orange--text">Language:</span> {{movie.original_language}}</div>
            <div class="white--text body-1"><span class="orange--text">Rating:</span> {{movie.vote_average}}</div>
            <div class="white--text body-1"><span class="orange--text">Popularity:</span> {{movie.popularity}}</div>

            <div class="white--text body-1 pb-6" v-if="movie"><span class="orange--text">Production companies: </span> 
                <span v-for="(comp, index) in companies" :key="index">{{ comp }}<span 
                    v-if="index !== companies.length - 1">, </span>
                </span>.
            </div>

            <v-divider></v-divider>
            <div class="white--text pt-6 pb-6 body-1">{{ movie.overview }}</div>
            <v-divider></v-divider>

        </v-card-text>

        <v-card-actions>
        <v-btn
            color="orange"
            text
            @click.prevent="goBack"
        >
            Back
        </v-btn>
        </v-card-actions>
    </v-card>

    </div>
</template>

<script>
import axios from 'axios'
const key = "dbc9fd3cb8c02c485593e9bf8ba731d7";


export default {
    props: ['guestId'],

    data() {
        return {
            rating: 0,
            movie: "",
            url: "",
            movieTitle: "",
            movieDate: "",
            ratedMovies: []
        }
    },
    created() {
        const id = this.$route.params.movieId
        axios
            .get(`https://api.themoviedb.org/3/movie/${ id }?api_key=${ key }`)
            .then(resp => {
                console.log(resp.data)
                this.movie = resp.data
                this.url = resp.data.backdrop_path
                console.log(id)

            })
        axios
            .get(`https://api.themoviedb.org/3/guest_session/${ this.guestId }/rated/movies?api_key=${ key }&language=en-US&sort_by=created_at.asc`)
            .then(resp => {
                console.log(resp.data.results)
                this.ratedMovies = resp.data.results
            })
    },
    methods: {
        onRatingClick() {
            const id = this.$route.params.movieId
            console.log(this.guestId)
            axios
                .post(`https://api.themoviedb.org/3/movie/${ id }/rating?api_key=${ key }&guest_session_id=${ this.guestId }`, {
                    value: this.rating
                })
                .then(resp => {
                    console.log(resp)
                })

        },
        goBack() {
            this.$router.go(-1)
        }
    },
    computed: {
        backdrop: function() {
            return `https://image.tmdb.org/t/p/original${ this.movie.backdrop_path }`  
        },
        companies: function() {
            const companiesList = this.movie.production_companies.map(comp => {
                return comp.name
            })
            return companiesList
        }
    },
    watch: {
        movie: function() {
            if(this.movie.release_date) {
                this.movieTitle = this.movie.title + " (" + this.movie.release_date.slice(0, 4) + ")"
                this.movieDate = this.movie.release_date.split("-").reverse().join(".") + '.'
            } else {
                this.movieTitle = this.movie.title
                this.movieDate = "Unknown"
            }
            
        },
        ratedMovies() {
            const id = this.$route.params.movieId
            this.ratedMovies.forEach(movie => {
                if(movie.id == id) {
                    this.rating = movie.rating
                }
            })
        }
    }
}
</script>

<style lang="sass" scoped>
 
    #cardContainer
        background-color: #333
        // border: 1px solid orangered
        padding: 30px
        min-height: calc(100vh - 64px)
    #cardImage
        border-bottom: 1px solid orange
        border-top: 1px solid orange


  
</style>