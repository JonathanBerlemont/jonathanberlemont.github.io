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
            :title="experience.title"
            :subtitle="`${experience.started} - ${experience.finished}`"
            color="#00ff66"
            variant="outlined"
            class="mb-5"
        >
        <template #prepend>
            <img :src="`/logos/${experience.logo}`" style="width: 150px;" />
        </template>
        </v-card>
    </div>

</template>

<style scoped>
    
</style>