<script lang="ts" setup>
import experiences from "@/data/experiences.json";
</script>

<template>
    <div class="ascii-container">
        <pre class="ascii-text">
  ______                      _                     
 |  ____|                    (_)                    
 | |__  __  ___ __   ___ _ __ _  ___ _ __   ___ ___ 
 |  __| \ \/ / '_ \ / _ \ '__| |/ _ \ '_ \ / __/ _ \
 | |____ >  <| |_) |  __/ |  | |  __/ | | | (_|  __/
 |______/_/\_\ .__/ \___|_|  |_|\___|_| |_|\___\___|
             | |                                    
             |_|                                    
        </pre>
    </div>

        <div class="experiences">
            <v-card
                v-for="experience in experiences"
                :key="experience.title"
                color="#00ff66"
                variant="outlined"
                class="mb-5"
            >
                <template #append>
                    <div style="border: 1px solid currentColor; border-radius: 5px; padding: 8px 12px; background-color: color-mix(in srgb, currentColor 15%, transparent);">
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

                    <div class="tags">
                        <v-chip
                            v-for="tag in experience.tags"
                            :key="tag"
                            size="small"
                            variant="outlined"
                            class="mr-1"
                        >
                            {{ tag }}
                        </v-chip>
                    </div>
                </v-card-text>
            </v-card>
        </div>

</template>

<style scoped>

</style>