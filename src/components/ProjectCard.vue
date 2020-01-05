<template>
    <v-card
            max-width="344"
            class="mx-auto card-outter"
            hover height="100%"
    >
        <v-list-item>
            <v-list-item-content>
                <v-alert type="success">
                    {{project.name}}
                </v-alert>
            </v-list-item-content>
        </v-list-item>

        <v-carousel
                height=200 class="bg-red">
            <v-carousel-item
                    v-for="(image,i) in images_list"
                    :key="i"
                    :src="image"
                    reverse-transition="fade-transition"
                    transition="fade-transition"
            ></v-carousel-item>
        </v-carousel>

        <v-card-text>
            <div class="text--primary text-justify font-weight-bold">
                {{project.description}}
            </div>

            <v-divider class="mx-4 mt-4 mb-4"></v-divider>

            <div class="text--primary text-right">
                {{project.technology}}
            </div>

        </v-card-text>

        <v-card-actions class="card-actions">
            <v-btn
                    text
                    color="deep-purple accent-4"
                    :href="project.link_github" target="_blank"
            >
                <v-icon left>mdi-github-circle</v-icon>
                Github
            </v-btn>

            <v-spacer v-if="project.link"></v-spacer>

            <v-btn
                    v-if="project.link"
                    text
                    color="deep-purple accent-4"
                    :href="project.link" target="_blank"
            >
                <v-icon left>mdi-share</v-icon>
                Ссылка на результат
            </v-btn>
        </v-card-actions>

    </v-card>
</template>

<script>
    export default {
        props: {
            project: Object
        },
        data() {
            return {
                baseUrl: process.env.VUE_APP_BASE_URL,
                images_list: [],
                bottomNav: 'recent',
            }
        },
        mounted() {
            const images = this.project.images;
            for (let i = 0; i < images.length; i++) {
                this.images_list.push(this.baseUrl + 'project_images/' + images[i]);
            }
        },
    };
</script>

<style scoped>
    .card-outter {
        position: relative;
        padding-bottom: 50px;
    }
    .card-actions {
        position: absolute;
        bottom: 0;
    }
</style>