<script lang="ts" setup>
import TagList from "@/components/TagList.vue";
import projects from "@/data/projects.json";
</script>

<template>
    <h2 class="ascii-container">
        <span class="d-sr-only">QA Artifacts</span>
        <pre class="ascii-text" aria-hidden="true">
   ____                               _   _  __           _       
  / __ \     /\            /\        | | (_)/ _|         | |      
 | |  | |   /  \          /  \   _ __| |_ _| |_ __ _  ___| |_ ___ 
 | |  | |  / /\ \        / /\ \ | '__| __| |  _/ _` |/ __| __/ __|
 | |__| | / ____ \      / ____ \| |  | |_| | || (_| | (__| |_\__ \
  \___\_\/_/    \_\    /_/    \_\_|   \__|_|_| \__,_|\___|\__|___/
                                                                  
                                                                  
        </pre>
    </h2>

    <div class="projects">
        <v-card
            v-for="project in projects"
            :key="project.title"
            color="#00ff66"
            variant="outlined"
        >
            <template #title>
                {{ project.title }}
            </template>
            <template #append>
                <v-btn target="_blank" rel="noopener noreferrer" :href="project.link" :append-icon="project.type == 'file' ? 'mdi-download' : 'mdi-open-in-new'" color="#00ff66" variant="outlined">
                    {{ project.link_text ?? project.link }}
                </v-btn>
            </template>

            <v-card-text class="d-flex flex-column">
                <p class="mb-3">{{ project.description }}</p>

                <tag-list :tags="project.tags" />
            </v-card-text>
        </v-card>
    </div>

</template>

<style scoped>
p {
    color: white;
}

.projects {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
    @media (max-width: 768px) {
        grid-template-columns: 1fr;
    }
}

.projects :deep(.v-card) {
    display: flex;
    flex-direction: column;
}

.projects :deep(.v-card-text) {
    flex: 1;
    display: flex;
    flex-direction: column;
}
</style>