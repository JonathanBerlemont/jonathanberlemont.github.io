<script lang="ts" setup>
import skills from '@/data/skills.json';
</script>

<template>
    <h2 class="ascii-container">
        <pre class="ascii-text">
   _____ _    _ _ _     
  / ____| |  (_) | |    
 | (___ | | ___| | |___ 
  \___ \| |/ / | | / __|
  ____) |   <| | | \__ \
 |_____/|_|\_\_|_|_|___/
        </pre>
    </h2>
    <div class="d-flex flex-wrap ga-3 justify-center">
        <v-chip
            v-for="skill, index in skills"
            :prepend-icon="index<5 ? 'mdi-star' : ''"
            :variant="index<5 ? 'elevated' : 'tonal'"
            :key="skill"
            color="#00ff66"
            >
            {{ skill }}
        </v-chip>
    </div>
</template>