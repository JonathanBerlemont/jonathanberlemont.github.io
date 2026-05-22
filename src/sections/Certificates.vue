<script lang="ts" setup>
import certificates from '@/data/certificates.json';
</script>

<template>
    <div class="ascii-container">
        <pre class="ascii-text">
   _____          _   _  __ _           _   _                 
  / ____|        | | (_)/ _(_)         | | (_)                
 | |     ___ _ __| |_ _| |_ _  ___ __ _| |_ _  ___  _ __  ___ 
 | |    / _ \ '__| __| |  _| |/ __/ _` | __| |/ _ \| '_ \/ __|
 | |___|  __/ |  | |_| | | | | (_| (_| | |_| | (_) | | | \__ \
  \_____\___|_|   \__|_|_| |_|\___\__,_|\__|_|\___/|_| |_|___/
        </pre>
    </div>
    <div class="certificates">
        <v-card
            v-for="certificate in certificates"
            :key="certificate.name"
            :title="certificate.name"
            variant="outlined"
            color="#00ff66"
        >
            <template #prepend>
                <img :src="`/logos/${certificate.logo}`" style="width: 50px; height: 50px; object-fit: contain;" />
            </template>
            <template #append>
                <a :href="certificate.url" target="_blank" rel="noopener noreferrer">
                    <v-icon icon="mdi-open-in-new" color="#00ff66" />
                </a>
            </template>
        </v-card>
    </div>
</template>

<style scoped>
.certificates {
    display: grid;
    grid-template-columns: 1fr 1fr;
    .v-card {
        margin: 20px;
    }
}
</style>