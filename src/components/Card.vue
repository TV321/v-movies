<template>
        <v-card
            class="d-flex flex-column"
            max-width="300"
            height="600"
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

            <v-card-title ><div class="green-text">{{ movie }}</div></v-card-title>

            <v-card-subtitle class="pb-0">Number 10</v-card-subtitle>

            <v-card-text class="flex-grow-1">
            <div class="white--text">Whitehaven Beach</div>

            <div class="white--text">Whitsunday Island, Whitsunday Islands</div>
            </v-card-text>

            <v-card-actions>
            <v-btn
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
            </v-btn>
            </v-card-actions>
            
        </v-card>
</template>

<script>
export default {
    props: {
        movie: String,
        cardImg: String
    },
    data() {
        return {
            imageUrl: `https://image.tmdb.org/t/p/w500${ this.cardImg }`
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