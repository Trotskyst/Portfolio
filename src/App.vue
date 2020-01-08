<template>
    <v-app>
        <v-layout wrap class="d-flex cards">
            <v-card
                    width="344"
                    hover
                    class="pa-2 mx-2 card-outter"
                    v-for="(project, index) in project_list" :key="index"
            >
                <ProjectCard :project="project"/>
            </v-card>
        </v-layout>
    </v-app>
</template>

<script>
    import ProjectCard from '@/components/ProjectCard'
    import axios from 'axios'

    export default {
        components: {
            ProjectCard,
        },
        data() {
            return {
                baseUrl: process.env.VUE_APP_BASE_URL,
                project_list: null,
            }
        },
        methods: {
            async getProjectList() {
                await axios.get(this.baseUrl + 'project_list.json').then(response => {
                    this.project_list = response.data;
                });
            }
        },
        created() {
            this.getProjectList();
        }
    }
</script>

<style scoped>
    .cards {
        flex: 0 0 auto;
    }
</style>