<template>
        <v-card
            :to="'/details/' + movieId"
            class="d-flex flex-column"
            width="300"
            height="550"
            link
            dark
            hover
        >
            <v-img
                v-if="cardImg"
                class="white--text align-start"
                max-height="350px"
                :src="fullImageUrl"
            >
            </v-img>
            <v-img
                v-else
                class="white--text align-start"
                max-height="350px"
                src="@/assets/movie.jpg"
            >
            </v-img>

            <v-card-title ><div >{{ fullTitle }}</div></v-card-title>

            <v-card-subtitle class="pb-0 flex-grow-1">Language: {{ lang }} </v-card-subtitle>

            <v-card-actions>
 
                <v-spacer></v-spacer>
                <v-avatar color="#333" size="50" style="border: 3px solid #101010">
                    <span class="orange--text headline">{{rating}}</span>
                </v-avatar>
            </v-card-actions>
            
        </v-card>
</template>

<script>
export default {
    props: {
        movie: String,
        cardImg: String,
        date: String,
        lang: String,
        rating: Number,
        index: Number,
        movieId: Number
    },
    computed: {
        fullTitle: function() {
            return this.movie + " " + "(" + this.date.slice(0, 4) + ")"
        },
        fullImageUrl() {
            return 'https://image.tmdb.org/t/p/w500' + this.cardImg
        }
    }
}
</script>

<style lang="sass" scoped>
    div.v-card
        // border: 1px solid orangered
        
    // .v-responsive
    //     flex: unset
    div.v-card__title
        color: #FFC107

        
</style>