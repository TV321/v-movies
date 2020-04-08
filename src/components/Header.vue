<template>
    <v-app-bar color=#222 style="border-bottom: 1px solid #ff9800">
        <v-btn icon>
            <v-icon>mdi-heart</v-icon>
        </v-btn>
        <v-toolbar-title><span class="orange--text">{{ title }}</span></v-toolbar-title>
        <v-spacer></v-spacer>

    </v-app-bar>
</template>

<script>
export default {
    props: {
        title: String
    }
}
</script>
<style lang="sass" scoped>

    // div.v-toolbar__title
    //     color: #ff9800
    header.v-toolbar.v-app-bar
        box-shadow: none

</style>    