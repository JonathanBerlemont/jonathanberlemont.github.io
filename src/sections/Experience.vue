<script lang="ts" setup>
import TagList from "@/components/TagList.vue";
import experiences from "@/data/experiences.json";
</script>

<template>
    <h2 class="ascii-container">
        <span class="d-sr-only">Experience</span>
        <pre class="ascii-text" aria-hidden="true">
  ______                      _                     
 |  ____|                    (_)                    
 | |__  __  ___ __   ___ _ __ _  ___ _ __   ___ ___ 
 |  __| \ \/ / '_ \ / _ \ '__| |/ _ \ '_ \ / __/ _ \
 | |____ >  <| |_) |  __/ |  | |  __/ | | | (_|  __/
 |______/_/\_\ .__/ \___|_|  |_|\___|_| |_|\___\___|
             | |                                    
             |_|                                    
        </pre>
    </h2>

    <div class="experiences">
        <v-card
            v-for="experience in experiences"
            :key="experience.title"
            color="#00ff66"
            variant="outlined"
            class="mb-5"
        >
            <template #append>
                <div class="company-logo" style="border: 1px solid currentColor; border-radius: 5px; padding: 8px 12px; background-color: color-mix(in srgb, currentColor 15%, transparent);">
                    <img :src="`/logos/${experience.logo}`" style="width: 120px; object-fit: contain;" />
                </div>
            </template>

            <template #title>
                {{ experience.title }}
            </template>

            <template #subtitle>
                {{ experience.company }} · {{ experience.started }} – {{ experience.finished }}
            </template>

            <v-card-text>
                <p class="mb-3">{{ experience.description }}</p>

                <ul class="bullets mb-3">
                    <li v-for="bullet in experience.bullets" :key="bullet">
                        {{ bullet }}
                    </li>
                </ul>
                
                <v-dialog max-width="800" v-if="experience.highlights">
                    <template #activator="{ props }">
                        <v-btn color="#00ff66" variant="outlined" class="mb-3" v-bind="props" append-icon="mdi-creation">
                            Projects Highlights
                        </v-btn>
                    </template>

                    <v-card color="#00ff66" variant="outlined" class="highlight-card">
                        <template #title>
                            {{ experience.company }} — Highlights
                        </template>
                        <v-card-text>
                            <ul>
                                <li
                                    v-for="highlight in experience.highlights" 
                                    :key="highlight.url"
                                    class="mb-5"
                                >
                                    <v-btn
                                        :href="highlight.url"
                                        target="_blank"
                                        rel="noopener noreferrer"
                                        variant="outlined"
                                        color="#00ff66"
                                        append-icon="mdi-open-in-new"
                                    >
                                        {{highlight.url }}
                                    </v-btn>
                                    <p>{{ highlight.description }}</p>
                                </li>
                            </ul>
                            
                        </v-card-text>
                    </v-card>
                </v-dialog>

                <TagList :tags="experience.tags" />

            </v-card-text>
        </v-card>
    </div>

</template>

<style scoped>
@media (max-width: 768px) {
    .v-card .company-logo {
        display: none;
    }
}
p, ul {
    color: white;
}
.highlight-card {
    background-color: black;
    ul {
        list-style: none;
        padding-left: 0;

        li:not(:last-child) { border-bottom: solid 1px #006633; }
    }
}
</style>