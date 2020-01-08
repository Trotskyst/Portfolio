<template>
    <div>
        <v-list-item>
            <v-list-item-content>
                <v-alert type="success">
                    {{project.name}}
                </v-alert>
            </v-list-item-content>
        </v-list-item>

        <v-carousel v-if="images_list.length > 0"
                    height=200 class="bg-red">
            <v-carousel-item
                    v-for="(image,i) in images_list"
                    :key="i"
                    :src="image"
                    reverse-transition="fade-transition"
                    transition="fade-transition"
            ></v-carousel-item>
        </v-carousel>

        <v-card-text class="mb-5">
            <div class="text--primary text-justify font-weight-bold">
                {{project.description}}
            </div>

            <v-divider class="mx-4 mt-4 mb-4"></v-divider>

            <div class="text--primary text-right">
                {{project.technology}}
            </div>

        </v-card-text>

        <v-card-actions class="card-actions">
            <ProjectCardBottomButton v-if="project.link_github" :link=project.link_github :icon="icon_Github"
                                     :text="text_Github"/>

            <ProjectCardBottomButton v-if="project.link" :link=project.link :icon="icon_result" :text="text_result"/>
        </v-card-actions>

    </div>
</template>

<script>
    import ProjectCardBottomButton from "@/components/ProjectCardBottomButton";

    export default {
        props: {
            project: Object
        },
        components: {
            ProjectCardBottomButton,
        },
        data() {
            return {
                baseUrl: process.env.VUE_APP_BASE_URL,
                images_list: [],
                bottomNav: 'recent',
                icon_Github: 'mdi-github-circle',
                icon_result: 'mdi-share',
                text_Github: 'Github',
                text_result: 'Результат',
            }
        },
        mounted() {
            const images = this.project.images;
            if (images) {
                for (let i = 0; i < images.length; i++) {
                    this.images_list.push(this.baseUrl + 'project_images/' + images[i]);
                }
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