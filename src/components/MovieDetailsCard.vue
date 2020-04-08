<template>
    <div id="cardContainer">
    <v-card
        dark
        class="mx-auto"
        max-width="700"
    >
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
        
        <v-card-title class="amber--text headline">{{ movieTitle }}</v-card-title>
        <v-card-subtitle class="pb-3 subtitle-1">Release date: {{ movieDate }}</v-card-subtitle>

        <v-card-text class="text--primary">
            <div class="white--text body-1"><span class="orange--text">Language:</span> {{movie.original_language}}</div>
            <div class="white--text body-1"><span class="orange--text">Rating:</span> {{movie.vote_average}}</div>
            <div class="white--text body-1"><span class="orange--text">Popularity:</span> {{movie.popularity}}</div>

            <div class="white--text body-1" v-if="movie"><span class="orange--text">Production companies: </span> 
                <span v-for="(comp, index) in companies" :key="index">{{ comp }}<span 
                    v-if="index !== companies.length - 1">, </span>
                </span>.
            </div>

            <div class="white--text pt-6 body-1">{{ movie.overview }}</div>

        </v-card-text>

        <v-card-actions>
        <v-btn
            color="orange"
            text
            to="/"
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
    
    data() {
        return {
            movie: "",
            url: "",
            movieTitle: "",
            movieDate: ""
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
            this.movieTitle = this.movie.title + " (" + this.movie.release_date.slice(0, 4) + ")"
            this.movieDate = this.movie.release_date.split("-").reverse().join(".") + '.'
        }
    }
}
</script>

<style lang="sass" scoped>
 
    #cardContainer
        background-color: #333
        border: 1px solid orangered
        padding: 30px
        min-height: calc(100vh - 64px)


  
</style>