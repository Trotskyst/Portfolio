<template>
    <v-btn
            text
            color="deep-purple accent-4"
            :href="link" target="_blank"
    >
        <v-icon left>
            {{icon}}
        </v-icon>
        {{text}}
    </v-btn>
</template>

<script>
    export default {
        props: {
            link: String,
            icon: String,
            text: String
        }
    }
</script>