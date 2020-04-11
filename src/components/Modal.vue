<template>
  <div>
    <v-dialog
      v-model="dialog"
      width="500"
      
    >
      <template v-slot:activator="{ on }">
        <v-btn light fab color="#FFC107" v-on="on">
            <v-icon>mdi-all-inclusive</v-icon>
        </v-btn>
      </template>

      <v-card>
        <v-card-title
          class="headline orange grey--text text--darken-4"
          primary-title
        >
          Random Movie by Genre
        </v-card-title>

        <v-card-text class="pt-2">
            <v-radio-group v-model="inputValue" column @change="onInput">
            <v-radio label="Action" value="28" color="orange"></v-radio>
            <v-radio label="Crime" value="80" color="orange"></v-radio>
            <v-radio label="Comedy" value="35" color="orange"></v-radio>
            <v-radio label="Horror" value="27" color="orange"></v-radio>
            <v-radio label="Science Fiction" value="878" color="orange"></v-radio>
          </v-radio-group>
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-btn
            :to="'/details/' + movieId"
            block
            color="orange"
            text
            @click="dialog = false, inputValue = ''"
            :disabled="inputValue == ''"
          >
            Roll
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import axios from 'axios'
const key = "dbc9fd3cb8c02c485593e9bf8ba731d7"

  export default {
    data () {
      return {
        dialog: false,
        inputValue: '',
        movieId: 419704,
        movies: [],
      }
    },
    methods: {
        onInput() {
            let randomPage = Math.floor(Math.random() * 500) + 1
            axios
                .get(`https://api.themoviedb.org/3/discover/movie?api_key=${ key }&language=en-US&sort_by=popularity.desc&include_adult=false&include_video=false&page=${ randomPage }&with_genres=${ +this.inputValue }`)
                .then(resp => {
                    console.log(resp.data.results)
                    this.movies = resp.data.results
                })
        },
    },
     watch: {
            movies: function() {
                let randomMovie = Math.floor(Math.random() * this.movies.length)
                this.movieId = this.movies[randomMovie].id
            }
        }
  }
</script>