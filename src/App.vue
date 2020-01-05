<template>
    <v-app>
        <v-container grid-list-sm>
            <v-layout wrap>
                <v-flex xs12 sm4 v-for="(project, index) in project_list" :key="index">
                    <ProjectCard :project="project"/>
                </v-flex>
            </v-layout>
        </v-container>
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
