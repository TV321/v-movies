<template>
        <v-card
            class="d-flex flex-column"
            max-width="300"
            height="550"
            link
            dark
            hover
        >
            <v-img
            class="white--text align-start"
            max-height="350px"
            :src="imageUrl"
            >
            
            </v-img>

            <v-card-title ><div class="green-text">{{ fullTitle }}</div></v-card-title>

            <v-card-subtitle class="pb-0 flex-grow-1">Language: {{ lang }}</v-card-subtitle>
<!-- 
            <v-card-text class="flex-grow-1">
                <div class="white--text">Whitehaven Beach</div>

                <div class="white--text">Whitsunday Island, Whitsunday Islands</div>
            </v-card-text> -->

            <v-card-actions>
                <!-- <v-btn
                    color="orange"
                    text
                >
                    Share
                </v-btn>

                <v-btn
                    color="orange"
                    text
                >
                    Explore
                </v-btn> -->
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
        rating: Number
    },
    data() {
        return {
            imageUrl: `https://image.tmdb.org/t/p/w500${ this.cardImg }`
        }
    },
    computed: {
        fullTitle: function() {
            return this.movie + " " + "(" + this.date.slice(0, 4) + ")"
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