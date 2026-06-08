<script lang="ts" setup>
import projects from "@/data/projects.json";
</script>

<template>
    <h2 class="ascii-container">
        <pre class="ascii-text">
  _____           _           _       
 |  __ \         (_)         | |      
 | |__) | __ ___  _  ___  ___| |_ ___ 
 |  ___/ '__/ _ \| |/ _ \/ __| __/ __|
 | |   | | | (_) | |  __/ (__| |_\__ \
 |_|   |_|  \___/| |\___|\___|\__|___/
                _/ |                  
               |__/                   
        </pre>
    </h2>

    <div class="projects">
        <v-card
            v-for="project in projects"
            :key="project.title"
            color="#00ff66"
            variant="outlined"
            class="mb-5"
        >
            <template #title>
                {{ project.title }}
            </template>
            <template #append>
                <v-btn target="_blank" rel="noopener noreferrer" :href="project.link" :append-icon="project.type == 'file' ? 'mdi-download' : 'mdi-open-in-new'" color="#00ff66" variant="outlined">
                    {{ project.link_text ?? project.link }}
                </v-btn>
            </template>

            <v-card-text>
                <p class="mb-3">{{ project.description }}</p>

                <div class="tags">
                    <v-chip
                        v-for="tag in project.tags"
                        :key="tag"
                        size="small"
                        class="ma-1"
                    >
                        {{ tag }}
                    </v-chip>
                </div>
            </v-card-text>
        </v-card>
    </div>

</template>

<style scoped>
p {
    color: white;
}
</style>