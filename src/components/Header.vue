<template>
    <v-app-bar color=#222 style="border-bottom: 1px solid #ff9800">
        <v-btn icon>
            <v-icon>mdi-heart</v-icon>
        </v-btn>
        <v-toolbar-title><span class="orange--text">{{ title }}</span></v-toolbar-title>
        <v-spacer></v-spacer>

        <v-toolbar-items>
            <v-row align="center" justify="end" class="mr-3">
            <v-col class="d-flex" cols="12" sm="6">
                <v-select
                    @change="onChange(inputValue)"
                    v-model="inputValue"
                    dense
                    v-if="title == 'MOVIES'"
                    dark
                    :items="items2"
                    label="SELECT"
                    outlined>
                </v-select>
            </v-col>
            </v-row>
        </v-toolbar-items>
        <v-btn icon>
            <v-icon>mdi-heart</v-icon>
        </v-btn>

        
    </v-app-bar>
</template>

<script>
export default {
    props: {
        title: String,
        display: String,
        onChange: Function
    },
    data() {
        return {
            items: ['Top Rated', 'Popular', 'Latest'],
            items2: [
                {
                    text: 'Top Rated', 
                    value: 'top_rated'
                }, 
                {
                    text: 'Popular', 
                    value: 'popular'
                }, 
                {
                    text: 'Now Playing', 
                    value: 'now_playing'
                }, 
            ],
            inputValue: ''
        }
    },
    mounted() {
        this.inputValue = this.display
    }
}
</script>
<style lang="sass" scoped>

    // div.v-toolbar__title
    //     color: #ff9800
    header.v-toolbar.v-app-bar
        box-shadow: none

</style>    